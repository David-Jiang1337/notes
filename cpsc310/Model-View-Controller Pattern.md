The model-view-controller (MVC) pattern is one of the oldest GUI design patterns. In the MVC pattern, the **model** represents the modules responsible for business logic, the **view** represents the graphical interface being displayed, and the **controller** facilitates interactions between the two.

Canonically, MVC is coupled as such:
- **Model** holds a reference to view only, where the model is the subject and the view is the observer. It uses this reference to inform view when the interface needs to be updated with new information. It is up to view to decide what to display and how to display it.
- **View** holds a reference to model and controller. It uses its reference to controller to pass along user input to be translated into business logic in model, and holds a reference the model so it can read the data it should display.
- **Controller** holds a reference to model only. When it receives input from view, it will inform the model of what business logic to execute.
For example, if a user wishes to search a database using a frontend designed via the MVC pattern, the text box and UI elements for data entries would be the view. When the user enters something into the text box to search, the view would send a message to the controller (likely with the contents of the text box), and the controller would then use that data to query the model, which in turn handles the search query logic. When the model completes its query, it notifies the view that its state has changed. The view then reads the updated data from model and updates accordingly.

# Benefits
MVC was designed based on the idea that the underlying business logic and the visual interface will evolve separately and independently of each other. For instance, a company may want to visually overhaul their website appearance without changing any of the underlying logic, or back-end developers may make major updates to the business logic but the user experience should stay the same. As such, MVC has the following benefits:
- **Single Responsibility Principle**: the GUI implementation is split into three distinct responsibilities.
- **Open/Closed Principle**: both view and model can be extended without needing to make changes to the other.
as a result of these benefits, the GUI can be changed and improved without affecting the model, and less coordination is required between teams to make changes to the UI.

# Challenges
MVC remains a somewhat vague design pattern where all the different elements are still coupled to each other even if loosely. This ambiguity means that, in practice, the view often grows with complexity, taking on more and more presentation responsibilities that should ideally be shared with controller, as the UI coordination logic does clearly belong in controller or view specifically. 

Furthermore, MVC components can be difficult to test in isolation as controllers depend on concrete views and UI frameworks. 