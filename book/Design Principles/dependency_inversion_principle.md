# Dependency Inversion Principle

```
High-level modules should not depend on low-level modules. Both should depend on abstractions.

Abstractions should not depend on details. Details should depend on abstractions.
```

## Summary

*Dependency Inversion Principle* states that we should decouple high level modules from low level modules, introducing an abstraction layer between the high level classes and low level classes. Further more it inverts the dependency: instead of writing our abstractions based on details, the we should write the details based on abstractions.

*Dependency Inversion* or *Inversion of Control* are better know terms referring to the way in which the dependencies are realized. In the classical way when a software module(class, framework, etc.) need some other module, it initializes and holds a direct reference to it. This will make the 2 modules tight coupled. In order to decouple them the first module will provide a hook(a property, parameter, etc.) and an external module controlling the dependencies will inject the reference to the second one.

By applying the *Dependency Inversion* the modules can be easily changed by other modules just changing the dependency module. [Factories](TODO: add link) and [Abstract Factories](TODO: add link) can be used as dependency frameworks, but there are specialized frameworks for that, known as *Inversion of Control Container.*

## Motivation

When we design software applications we can consider the low level classes the classes which implement basic and primary operations(disk access, network protocols,...) and high level classes the classes which encapsulate complex logic(business flows, ...). The last ones rely on the low level classes. A natural way of implementing such structures would be to write low level classes and once we have them to write the complex high level classes. Since high level classes are defined in terms of others this seems the logical way to do it. But this is not a flexible design. What happens if we need to replace a low level class?

Let's take the classical example of a copy module which reads characters from the keyboard and writes them to the printer device. The high level class containing the logic is the Copy class. The low level classes are KeyboardReader and PrinterWriter.

In a bad design the high level class uses directly and depends heavily on the low level classes. In such a case if we want to change the design to direct the output to a new FileWriter class we have to make changes in the Copy class. (Let's assume that it is a very complex class, with a lot of logic and really hard to test).

In order to avoid such problems we can introduce an abstraction layer between high level classes and low level classes. Since the high level modules contain the complex logic they should not depend on the low level modules so the new abstraction layer should not be created based on low level modules. Low level modules are to be created based on the abstraction layer.

According to this principle the way of designing a class structure is to start from high level modules to the low level modules: 

```mermaid
flowchart LR
    id1[High Level Classes] --> id2[Abstraction Layer] --> id3[Low Level Classes]
```

## Intent
-   High-level modules should not depend on low-level modules. Both should depend on abstractions.
-   Abstractions should not depend on details. Details should depend on abstractions.

## Example

Below is an example which violates the Dependency Inversion Principle. We have the manager class which is a high level class, and the low level class called Worker. We need to add a new module to our application to model the changes in the company structure determined by the employment of new specialized workers. We created a new class SuperWorker for this.

Let's assume the Manager class is quite complex, containing very complex logic. And now we have to change it in order to introduce the new SuperWorker. Let's see the disadvantages:

-   we have to change the Manager class (remember it is a complex one and this will involve time and effort to make the changes).
-   some of the current functionality from the manager class might be affected.
-   the unit testing should be redone.

All those problems could take a lot of time to be solved and they might induce new errors in the old functionlity. The situation would be different if the application had been designed following the Dependency Inversion Principle. It means we design the manager class, an IWorker interface and the Worker class implementing the IWorker interface. When we need to add the SuperWorker class all we have to do is implement the IWorker interface for it. No additional changes in the existing classes.

```java
// Dependency Inversion Principle - Bad example
class Worker {
	public void work() {
		// ....working
	}
}

class Manager {
	Worker worker;

	public void setWorker(Worker w) {
		worker = w;
	}

	public void manage() {
		worker.work();
	}
}

class SuperWorker {
	public void work() {
		//.... working much more
	}
}
```

Below is the code which supports the Dependency Inversion Principle. In this new design a new abstraction layer is added through the IWorker Interface. Now the problems from the above code are solved(considering there is no change in the high level logic):

-   Manager class doesn't require changes when adding SuperWorkers.
-   Minimized risk to affect old functionality present in Manager class since we don't change it.
-   No need to redo the unit testing for Manager class.

```java
// Dependency Inversion Principle - Good example
interface IWorker {
	public void work();
}

class Worker implements IWorker {
	public void work() {
		// ....working
	}
}

class SuperWorker implements IWorker {
	public void work() {
		//.... working much more
	}
}

class Manager {
	IWorker worker;

	public void setWorker(IWorker w) {
		worker = w;
	}

	public void manage() {
		worker.work();
	}
}
```

## Conclusion

When this principle is applied it means the high level classes are not working directly with low level classes, they are using interfaces as an abstract layer. In this case instantiation of new low level objects inside the high level classes(if necessary) can not be done using the operator new. Instead, some of the Creational design patterns can be used, such as Factory Method, Abstract Factory, Prototype.

The [Template Design Pattern](TODO: add url) is an example where the DIP principle is applied.

Of course, using this principle implies an increased effort, will result in more classes and interfaces to maintain, in a few words in more complex code, but more flexible. This principle should not be applied blindly for every class or every module. If we have a class functionality that is more likely to remain unchanged in the future there is not need to apply this principle.

## Tags

#principle 
