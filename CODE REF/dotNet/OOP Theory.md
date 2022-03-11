## What is OOP
```c#
/*
	> It's a way of programming based on the concepts of objects.
*
```

## Why Object-Oriented Programming?
```c#
/*
	> OOP helps us to think in terms of real-world objects.
		- For example in a hospital, there are doctors and patients, we can create classes for each of them
		  and have a doctor class field inside of the patient class, expressing their relationship.
*
```

## Pros OOP?
```c#
/*
	> Abstraction, show only what is necessary.
	> Polymorphism, object acts differently user different conditions, i.e. a user object can become an employee or a customer.
	> Inheritance, Parent-child relationship.
	> Encapsulation, Hiding complexity.
*
```

## What are classes & objects?
```c#
/*
	> Class is a blueprint, a template where we can define attributes and methods.
	> An object is an instance of a class.
	> If we want to use a class we must create an instance of it.
*
```

## Explain Abstraction & Encapsulation
```c#
/*
	> Abstraction is to show only what is necessary.
	> Encapsulation is to hide complexity.
*
```

## Differentiate Abstraction & Encapsulation
```c#
/*
	> Using encapsulation we achieve Abstraction, they complement each other.
	> Abstraction occurs during the design phase while encapsulation is implemented during the development to achieve said abstraction.
*
```

## Explain inheritance
```c#
/*
	> Inheritance defines a parent-child or 'IS-A' relationship between two classes.
*
```

## Explain virtual & Overriding
```c#
/*
	> Virtual keywork allows a method to be overridden by the child if it wishes to.
	> Overring is the process of modifying existing logic inherited from a parent.
*
```

## Explain method overloading
```c#
/*
	> Same method names with different signatures in the same class.
*
```

## What is polymorphism
```c#
/*
	> It is the ability for an object to act differently under different conditions.
		- i.e. A man at the same time is a father, a husband an employee.
*
```

## Can polymorphism work without inheritance?
```c#
/*
	> No, 
*
```

## Explain Static vs Dynamic polymorphism
```c#
/*
	> Static poly is implemented by method overloading
	> Dynamic poly is implemented by method overriding
*
```

## What is an Abstract class?
```c#
/*
	> Abstract class is a partially defined base class
*
```

## Why do we need Abstract classes?
```c#
/*
	> An abstract class allows you to create functionality that subclasses can implement or override.
*
```

## Are abstract methods virtual?
```c#
/*
	> Yes.
*
```

## Can we create an instance of an Abstract class?
```c#
/*
	> No.
*
```

## Is it compulsory to implement all Abstract methods?
```c#
/*
	> Yes.
*
```

## Why can't base classes replaces Abstract classes?
```c#
/*
	> Because we cant partially define a base class.
*
```

## Why use interface?
```c#
/*
	> To create a contract so that the user must adhere the rules of the interface.
	> Multi inheritance
*
```

## What is an interface?
```c#
/*
	> Interface is a contract, by having a contract we have better control on impact analysis, change management, and breaking changes.
*
```

## Can we write logic inside of interface?
```c#
/*
	> No.
*
```

## Can we define interface methods as private?
```c#
/*
	> No, it is set to public by default
*
```

## When changing an existing interface what's the best practice?
```c#
/*
	> Create a new interface with inheriting the exiting interface
*
```

## Why use multi-interface inheritance?
```c#
/*
	> To add new methods to an existing interface without breaking.
*
```

## Explain interface segregation?
```c#
/*
	> Classes are not forced to use unnecessary logic that they don't need.
*
```

## Can we create an instance of an interface?
```c#
/*
	> No
*
```

## Can we do multiple inheritances with Abstract classes?
```c#
/*
	> No
*
```

## Difference between Abstract class vs Interface?
```c#
/*
	> Interface has no logic while abstract class can have some logic
	> Interfaces are implemented while abstract classes are inherited
*
```
## Why do we need constructors?
```c#
/*
	> Constructor is a special method that is invoked when an object of a class is created.
*
```
## In parent-child which constructor fires first?
```c#
/*
	> Parent constructor is executed first.
*
```
## In parent-child which initializers(fields) fires first??
```c#
/*
	> Child's first then parents.
*
```
## How are static constructors executed in parent-child classes?
```c#
/*

*
```
## What is a static class?
```c#
/*
	> Static classes are sealed and therefore cannot be inherited
*
```

## What is a static field?
```c#
/*
	> only one instance of the field is created and it is shared by all its objects
*
```

## What is shadowing/method hiding?
```c#
/*
	> Child methods are hidden from parents during polymorphism.
*
```

## Explain overriding vs shadowing?
```c#
/*
	> Overriding is when you override some existing logic inherited by a parent class
	> Shadowing is hiding methods from superclass during polymorphism
*
```

## What is the Single responsibility principle (SOLID)
```c#
/*
	> A class should only solve one problem
	> Small is good, keep it simple
*
```

## What is the Open-closed principle (SOLID)
```c#
/*
	> A class should be open to extension, however, closed to modification
*
```

## What is the Liskov substitution principle (SOLID)
```c#
/*
	> If we substitute a type with one of its subtypes, the behavior should not change
*
```

## What is the Segregation principle (SOLID)
```c#
/*
	> Avoid making general interfaces, an interface should be specific.
*
```

## What is the Dependency Inversion principle (SOLID)
```c#
/*
	> Higher level classes should not know the implementation of low-level classes.
*
```
