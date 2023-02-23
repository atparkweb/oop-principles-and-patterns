# Single Responsibility Principle

```
A class should have only one reason to change.
```

## Summary

In this context a responsibility is considered to be one reason to change. This principle states that if we have two reasons to change for a class, we have to split the functionality into two classes. Each class will handle only one responsibility and if we need to make one change we are going to make it in the class which handles it. When we need to make a change in a class having more responsibilities the change might affect the other functionality of the classes.

Single Responsibility Principle was introduced Tom DeMarco in his book *Structured Analysis and Systems Specification*, 1979. Robert Martin reinterpreted the concept and defined the responsibility as a reason to change.

## Tags

#principle 