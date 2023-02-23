# Dependency Inversion Principle

```
High-level modules should not depend on low-level modules. Both should depend on abstractions.

Abstractions should not depend on details. Details should depend on abstractions.
```

## Summary

*Dependency Inversion Principle* states that we should decouple high level modules from low level modules, introducing an abstraction layer between the high level classes and low level classes. Further more it inverts the dependency: instead of writing our abstractions based on details, the we should write the details based on abstractions.

*Dependency Inversion* or *Inversion of Control* are better know terms referring to the way in which the dependencies are realized. In the classical way when a software module(class, framework, etc.) need some other module, it initializes and holds a direct reference to it. This will make the 2 modules tight coupled. In order to decouple them the first module will provide a hook(a property, parameter, etc.) and an external module controlling the dependencies will inject the reference to the second one.

By applying the *Dependency Inversion* the modules can be easily changed by other modules just changing the dependency module. [Factories](TODO: add link) and [Abstract Factories](TODO: add link) can be used as dependency frameworks, but there are specialized frameworks for that, known as *Inversion of Control Container.*

## Tags

#principle 
