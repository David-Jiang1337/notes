The model-view-viewmodel (MVVM) design pattern is based on the principle that the UI is a representation of the state of the model. In this design, the **Model** is bound solely to a **ViewModel** which is responsible for sending requests to model and representing model's data as a UI-ready state. The **View** then reads this state and displays the interface accordingly.

So the coupling of MVVM is as such:
- **Model** holds a reference to **ViewModel** to notify it of state changes
- **ViewModel** holds a reference to **Model** in order to request business behavior.
- **View** components have data bindings to states in **ViewModel** (e.g. a text box is bound to a state in **ViewModel** so whenever the text in the text box changes, **ViewModel** is updated to reflect the change automatically).

# Benefits
Since **View** is connected to **ViewModel** by data binding, **ViewModel** does not need a reference to **View**, so the two are loosely coupled. This is a form of separation of concerns and allows front-end developers to only worry about **View**, and back-end developers to only worry about **ViewModel** and **Model**.

# Component-Based Pattern
The component-based pattern is an evolution of MVVM which describes the **View** as being made of a hierarchy of reusable **components**. In component-based UIs, each **component** is responsible for some small subset of the **ViewModel**'s state, so that the entire **View** constitutes the entire state and all of its children represent a subset of their parents states. In this way, user event callbacks (like button clicks or changed text boxes) are propagated from child to parent until they reach the **ViewModel**, and changes in state are propagated down to children so that those child **components** can reflect state changes. 

## Benefits
The benefit of component-based patterns is the benefit of the object-oriented paradigm. By allowing inheritance of behaviors and properties, **components** are reusable, reducing code duplication. The atomic nature of individual **components** also helps fulfill the single-responsibility principle. Since **components** are always extensible with consistent boilerplate behavior, they scale well as the software grows more complex.

## Challenges
On the other hand, components add structural and conceptual complexity and can provide too much abstraction for simpler programs, running the risk of becoming overengineered.