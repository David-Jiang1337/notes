The model-view-presenter (MVP) pattern attempts to improve upon the [[Model-View-Controller Pattern|MVC]] pattern by more clearly defining the purpose of the controller, as well as reducing the view to a passive interface that sends information in primitives only. In MVP, the model no longer knows of the view at all, and is only coupled to the presenter. Likewise, the view no longer accesses any data from model, and only serves as an interface for the presenter, drawing whatever the presenter requests. 

Canonically, MVP is coupled as such:
- **Model** holds a reference to presenter to inform presenter of state changes.
- **View** holds a reference to presenter to inform presenter of user input.
- **Presenter** holds a reference to model to tell model to change its business logic, and also holds a reference to view to tell view what to display given the information it receives from model.

For example, if a user queries a database using a MVP patterned frontend, the view will receive that input and send it to the presenter. The presenter will then decide what the input from the view means, and call the relevant query logic in the model. Once complete, the model will notify the presenter of the results. The presenter will organize the data into UI elements and ask the view to draw them.

# Benefits
MVP better aligns with SOLID principles. In interacting with a interface exposed by view, instead of a concrete view object, MVP fulfills the dependency inversion principle. Furthermore, the presenter is much easier to test than the controller, as its output is no longer reflected by displayed elements but rather calls to view, so a mock view can be designed to look for the right requests given the inputs it provides.

# Challenges
Despite improving on MVC, MVP still struggles with a ballooning presenter as UI coordination logic becomes more complex.