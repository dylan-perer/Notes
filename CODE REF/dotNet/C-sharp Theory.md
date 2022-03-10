## Explain the difference between .NET & Csharp
```c#
/*
	> dotNET is a framework.
		- Collection of libaries & it has a runtime.
	> C# is a programming language.
*
```

## Differentiate between .NET Framework Vs .NET Core Vs .NET 5.0
```c#
/*
	> .NET Framework is the oldest and only runs on windows.
	> .NET Core is cross platform.
		- Big gains in performance
		- Modular packaging
		- Full CLI support
	> .NET 5 and onwards is the unification of .NET Framework & .NET Core.
*
```

## What is IL(Intermediate Language) Code?
```c#
/*
	> When a .NET project is built it gets compiled into IL code.
	> IL Code is partially compiled code.
*
```

## What is the use of JIT(Just in Time compiler)?
```c#
/*
	> When a .NET program is run JIT compiles IL code into Machine code.
*
```

## What is the benefit of compiling into IL code?
```c#
/*
	> IL enables the platform and CPU independence.
*
```

## Does .NET support more languages?
```c#
/*
	> Yes, i.e. f#, visual basic. And they all get compiled into the same IL code.
*
```

## What is CLR (Common Language Runtime)?
```c#
/*
	> CLR invokes JIT to compile IL Code.
	> Calls Garbage collector to clean unused allocations in memory.
*
```
## What is managed and unmanaged code?
```c#
/*
	> Code that runs under CRL execution environment is called managed code, i.e. c#
	> Unmanaged code executes outside of CLR control, i.e. c++
*
```

## What is the use of a Garbage Collector?
```c#
/*
	> Garbage collector is a background process that handles removing any unused memory allocations.
*
```

## Can Garbage Collector claim unmanaged objects?
```c#
/*
	> No!, it can only claim allocations that are made through CLR.
*
```

## What is the importance of CTS(Common types system)?
```c#
/*
	> CTS ensures data types defined in two different languages get compiled to a common data type.
*
```

## What is the importance of CLS?
```c#
/*
	> Set of guidelines to ensure cross-language integration.
*
```

## Explain the difference between Stack & Heap?
```c#
/*
	> They are both locations in memory.
	> Value types and pointers to reference types are stored in the stack.
	> Reference types are stored in the heap.
*
```

## What are Value types & Reference types?
```c#
/*
	> Value types are stored in the stack.
	> Reference types are stored in the heap.
*
```

## What is Boxing & Unboxing?
```c#
/*
	> Boxing is when a value type is converted to a reference type.
	> Unboxing is when a reference type is converted to a value type
*
```

## What is the consequence of boxing and unboxing?
```c#
/*
	> Impacts performance
		- Jumping from stack to heap & vice versa
*
```

## Explain Casting, Implicit & Explicit casting
```c#
/*
	> Casting is the process of converting a data type into an another
	> Implicit casting is when no data loss occurs, i.e. int to double
	> Explicit casting is when data loss can occur, i.e. double to int where you lose the decimals
*
```

## Explain the difference between Array and ArrayList?
```c#
/*
	> Array is a fixed size and strongly typed.
		- Better performance
	> ArrayList has a dynamic length and is not strongly typed.
		- It is slower than an array because boxing & unboxing
*
```

## What are generic collections?
```c#
/*
	> Are strongly typed and have a flexible length.
*
```

## What are Threads (Multithreading)?
```c#
/*
	> Allows code to execute parallelly.
*
```

## Difference between Thread & Task?
```c#
/*
	> Task is an abstraction of threading.
	> Tasks can return something, can be canceled, can be used with async-await.
	> Tasks utilize CPU better because it does not have thread affinity where it tries to run on the same core
	> Unless you are working with legacy code tasks are always better than threads
*
```

## How do we handle exceptions in C-sharp?
```c#
/*
	> Using try-catch blocks
*
```

## What is the need for finally?
```c#
/*
	> It is a block of code that is always executed whether there is an exception or not.
*
```

## What is the use of 'ref' Keyword?
```c#
/*
	 > with ref keyword you can pass values to a function or method as a reference
*
```

## What is the use of 'out' Keyword?
```c#
/*
	 > out keyword can be used to return multiple values from a function.
*
```

## What is the use of 'in' Keyword?
```c#
/*
	 > Using 'in' will make the argument passed into a function read-only.
*
```

## What is the need for Delegates?
```c#
/*
	> Delegate is a pointer to a function, a callback.
*
```

## Example of where you would have used a delegate?
```c#
/*
	> Streaming file data from a thread to the main thread.
*
```

## What is a multicast Delegate?
```c#
/*
	
*
```

## Titile?
```c#
/*
	
*
```

## Titile?
```c#
/*
	
*
```

## Titile?
```c#
/*
	
*
```

## Titile?
```c#
/*
	
*
```

## Titile?
```c#
/*
	
*
```

## Titile?
```c#
/*
	
*
```

## Titile?
```c#
/*
	
*
```

## Titile?
```c#
/*
	
*
```