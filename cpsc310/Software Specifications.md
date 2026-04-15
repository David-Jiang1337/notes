Software engineering is said to be an attempt to solve a wicked problem. That is to say, a problem that can only be defined once it has been solved. In this sense, software engineering is an iterative process where attempting to solve parts of a problem allows developers to further define the problem, which informs further. This iterative process is carried out by all stakeholders of a piece of software, including customers, developers, and managers, etc. Through the consensus gained in this process, software engineers can create a specification.

A specification describes what a system should do and criteria for what it means for the system to successfully do those things. Different specifications can be created for different stakeholders, only describing the parts of system behavior that matter to certain groups. In that sense, specifications constitute a type of abstraction, where details unnecessary to the target audience of the specification are hidden, and important details are highlighted. 

For example, the C specification is primarily targeted at developers for C compilers, and so it lays out what certain keywords should do and the expected behaviors of the system, because developers need to know such things, but says little about implementation details because that should be up to the discretion of the developers themselves.

Software specifications are typically described as a list of requirements, the sum of which constitutes the desired system.
# Requirements
Requirements are, as the name suggests, things that are needed in a system. In software, requirements generally fall into two categories: **functional** and **non-functional** requirements. 

Functional requirements describe what a does. For instance, the requirement that a school database system must be able to display a list of students sorted by name is a functional requirement, because fulfilling the requirement means adding functionality to the system.

On the other hand, non-functional requirements describe properties of a system that fulfills its functional requirements. For instance, a functional requirement for the previously described school database would be that the system needs to show the student list in colors with high contrast. We can see that this requirement takes for granted that a functional requirement is met, and then attributes properties like color to the outcome of that functional requirement.
## Properties of a Good Requirement
A good requirement should have the following properties:
- **Completeness**: a requirement should address all facets of the behavior it describes. Leaving edge cases undefined can lead to misunderstandings.
- **Consistency**: a requirement should not ask for things that contradict another requirement, as conflicts can make the specification impossible to implement and also leads to confusion between stakeholders.
- **Precision**: a requirement should use precise language that only has one clear interpretation because, again, we want to avoid confusion between stakeholders that arise from having different interpretations of the requirements.
- **Concision**: a requirement should be concise and not use more words to say something can be said in fewer, as it is possible that more long-winded requirements can actually increase the risk of imprecise and confusing language.

## Constraints
In addition to the most common **functional** and **non-functional requirements**, there may be other types of requirements gathered during elicitation. These include:
- **Design Constraints**: instead of specifying what the system must do, constraints often describe what the system must not do (e.g. break local laws, be too costly). Constraints more generally describe the boundaries of a system, like what languages it must be written in and which frameworks it must use.
- **Environmental Constraints**: software does not exist in a vacuum, and so environmental constraints seek to address how the new software must interact with existing systems (i.e. the environment). For instance, the software might need to work on older versions of Linux, as well as newer ones. This would constitute an environmental constraint.
- **Preferences**: preferences refer to the relative importance of other requirements, describing which requirements must be prioritized and which ones can wait to be implemented.

# The Stages of Building a Specification
As described at the beginning of this article, 