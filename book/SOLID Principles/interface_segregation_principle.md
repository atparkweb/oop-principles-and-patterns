# Interface Segregation Principle

```
Clients should not be forced to depend upon interfaces that they don't use.
```

## Summary

This principle teaches us to take care how we write our interfaces. When we write our interfaces we should take care to add only methods that should be there. If we add methods that should not be there, the classes implementing the interface will have to implement those methods as well. For example, if we create an interface called *Worker* and add a method *lunch break*, all the workers will have to implement it. What if the worker is a robot?

In conclusion, interfaces containing methods that are not specific to it are called *polluted* or *fat interfaces*. We should avoid them.

## Tags

#principle #interface