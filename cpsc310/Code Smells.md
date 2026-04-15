Code smells are logical patterns in code that are indicative of poor design and a likely violation of SOLID design principles. The presence of code smells represents the accumulation of technical debt, where the design choices that have previously been made have made it difficult to implement new features. If technical debt is the difference in time and effort it takes to add a new feature to the existing code base and the time and effort it takes to add the same feature to a hypothetically perfectly designed code base, code smells are the patterns of code that make our codebases deviate from what the best version of our code could be.

# Types of Code Smells
## Magic Numbers
Well-written code should almost never explicitly contain numbers not assigned a name. Numbers always represent something, and so we should write variables or macros representing the numbers we are using, to make those numbers more descriptive, as well as eliminating the need for shotgun surgery when we wish to change those numbers.

For example, this code block with magic numbers:
```c
double hydrostaticPressure(double density, double height) {
	return density * 9.81 * height; // 9.81 is a magic number
}

double potentialEnergy(double mass, double height) {
	return mass * 9.81 * height; // another instance of a magic number,
	// note that we would have to change this number in two places if we want to change the force of gravity.
}
```
Can be improved by setting the acceleration due to gravity to a macro:
```c
#define GRAVITY 9.81 // now we know what 9.81 actually represents!

double hydrostaticPressure(double density, double height) {
	return density * GRAVITY * height;
}

double potentialEnergy(double mass, double height) {
	return mass * GRAVITY * height;
}
```
## Long Methods
A long method code smell is when a method contains in-line multiple distinct functionalities. The implementation of long methods are often not sufficiently abstracted, and the code smell can be fixed by extracting each distinct part of the implementation to its own, smaller method. 

## Explanatory Comments
Well-written code uses descriptively named variables and is formatted to be easy to read. The need for explanatory comments, therefore, implies that the code itself is not sufficiently clear to convey what it is doing.

For instance, the explanatory comments in this excerpt
```c
float b = a * 100;
// b is the cost in dollars 'a' converted to cents.
float c = b / n;
// c is the average cost in cents per customer.
```
Would be unnecessary if the variables themselves were named more legibly. 
```c
#define CENTS_PER_DOLLAR 100
float totalCostInCents = totalCostInDollars * CENTS_PER_DOLLAR;
float avgCentCostPerCustomer = totalCostInCents / numCustomers;
```
If anything, the clearly named variables are actually more descriptive than the explanatory comments.

It is worth noting that explanatory comments may be acceptable if they explain why a certain design decision was made, rather than what the design does.

## Long Parameter List
The long parameter list code smell compasses both when a function has too many parameters and when the parameters are cumbersome to understand regardless of how many there are.

For instance, this code has a long parameter list code smell because there are too many parameters:
```c
course_t makeCourse(int id, char* name, int course_namelen, char* school, int school_namelen, int courseCode);
```
And this one doesn't have many parameters but can easily be confusing:
```c
void setTimeDate(int day, int month, int year); // day month year or month day year??
```

Both types of this code smell can be fixed by creating a type which contains all of the parameters the function needs:
```c
typedef timeDate {
	int day;
	int month;
	int year;
} timedate_t
void setTimeDate(timedate_t timeDate); // day month year or month day year??
```

## Switch Case on Type
Having switch cases in a module so that behavior may be determined by the type of an object is generally an indicator that it will be cumbersome to add new functionality to the module, as the switch case will have to be added to each time, and will quickly balloon in size to become unreadable. To fix this code smell, the functionality currently being determined by switch case should be implemented using polymorphism instead.

For instance, this class:
```typescript
class Bird {
	private type: string;
	
	public getSpeed(): int {
		switch(this.type) {
			case "Falcon":
				return 300;
			case "Seagull":
				return 100;
			default:
				return 0;
		}
	}
	
	constructor(type: string) {
		this.type = type;
	}
}
```
can be improved by subclassing:
```typescript
abstract class Bird {
	abstract public getSpeed(): int;
}

class Falcon extends Bird {
	public getSpeed() {
		return 300;
	}
}

class Seagull extends Bird {
	public getSpeed() {
		return 100;
	}
}
```

## Code Duplication
Code duplication is where similar logic is duplicated in multiple places, making changes more difficult to make as changes may need to be replicated for each code block that uses said repeated logic. Code duplication can be reduced by introducing a template method, where previously abstract methods in the superclass hold common logic:
```typescript
abstract class Person {
	abstract public introduce(): void;
}

class Bob extends Person {
	public introduce(): void {
		console.log("Hi!");
		console.log("My name is Bob,");
		console.log("Nice to meet you.");
		console.log("What is your name?");
	}
}

class Joe extends Person {
	public introduce(): void {
		// lots of duplicate content being printed
		console.log("Hi!"); 
		console.log("I'm Joe,");
		console.log("Nice to meet you.");
		console.log("What is your name?");
	}
}
```
the above code can be improved with template methods:
```typescript
abstract class Person {
	abstract private sayName(): void;
	public introduce(): void {
		console.log("Hi!");
		this.sayName();
		console.log("Nice to meet you.");
		console.log("What is your name?");
	}
}

class Bob extends Person {
	private sayName(): void {
		console.log("My name is Bob,"); 
		// we just eliminated three lines of code per function!
	}
}

class Joe extends Person {
	public sayName(): void {
		console.log("I'm Joe,");
	}
}
```

## Feature Envy
Feature envy is when the implementation of a method seeks to make many changes or calls to another class. This code smell indicates that the current method is not properly delegating tasks to the correct modules, and should seek to delegate what it is doing to the appropriate class. To illustrate the code smell, the law of Demeter states that if a method finds itself chaining a lot of dereferences, that part of the code is probably in the wrong class.
For example, the chain dereferences here:
```typescript
class Cat {
	private fido = new Dog();
	public chaseDog() {
		this.fido.run();
		this.fido.tail.wag(); // why is the cat wagging the dog's tail?
		this.fido.mouth.smile(); 
		// ... etc
	}
}
```
can be eliminated by delegating them to the actual class we are dereferencing:
```typescript
class Cat {
	private fido = new Dog();
	public chaseDog() {
		this.fido.beChased(); // implement a beChased method in Dog
	}
}
```

## Divergent Changes
Unlike many other code smells, divergent changes are not a pattern in the code, but a pattern of changes to said code. Specifically, the divergent changes code smell occurs when the developer finds themselves needing to repeatedly make changes to a class for varying, or unrelated reasons. This is often an indication that the class with divergent changes is trying to fulfill to many responsibilities at once and should be split up into multiple different classes.

## Shotgun Surgery
Shotgun surgery, like divergent changes, are a non-static code smell that occurs when attempting to make a single change requires making small changes in many different parts of the codebase. It is effectively the inverse of divergent changes, where instead of many changes happening to a single module, a single change impacts many modules. The need for shotgun surgery implies that many modules currently have a responsibility in common. To address this problem, developers should identify the commonality in the changes being made to the many modules and delegate that responsibility to a new module.