The facade design pattern is a structural pattern where an interface exposes but simplifies the functionality of a complex subsystem. 

A facade pattern should be used when many clients are using a complex set of modules, and serves the purpose of reducing complexity for clients by providing them with a simpler interface that is capable of the functionality of the subsystem, without requiring the clients to have to know of all of the types and specifications involved with each individual module of the subsystem. 

However, it is worth noting that a facade design pattern should not preclude the client from interacting with the subsystem directly should the client actively wish to do so, and so the modules that facade simplifies should still be visible.