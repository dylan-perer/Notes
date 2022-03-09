## .NET Core vs .NET Framework
```c#
/*
	> dotNET core is cross-platform where .NET Framework is windows only
	> Now they are both packaged together
*
```

## Language Vs Framework
```c#
/*
	> C# is a language
	> dotNET is a framework, you can think a framework as a big bag of libraries
*
```

## How .NET is Compiled
```c#
/*
	> our C# code gets converted to an INTERMEDIATE LANGUAGE(IL code) --- BUILD PROCESS
	> Then when the application actually runs JIT will come and compile IL code to machine code --- RUN PROGRAM

	> C# => NTERMEDIATE LANGUAGE(IL code) => JIT => (01100) Machine code
*
```

## .DLL
```c#
/*
	> DLL can be added as a dependency to other projects
	> Pure functionality code
	> No UI attached to it
*
```

## CTS (Common type system)
![[Screenshot 2022-03-06 190655.png]]

```c#
/*
	> it brings the data types to a common ground of different.NET languages
	> A integer defined in C#, F# or VB, when it compiled to the INTERMEDIATE LANGUAGE(IL) it is the same (i.e. int32)
*
```

## CLS (Common language specification)
```c#
/*
	> If we want to write a program that uses multiple.NET languages we have to follow a CLS
	> It GOVERNS WHAT TO DO and WHAT TO AVOID if we want to use MULTIPLE LANGUAGES in ONE program
*/
[assembly: CLSCompliant(true)]//we can add this decorator to get editor warnings to make out code CLS compliant
```

## Casting
```c#
/*
	> There are two types of casting
		- Implicit, no data loss
		- Explicit, some data loss
*/

double x = 1123.33;
int a = (int)x;

Console.WriteLine(a);
```
### Conversion
```c#
/*
	- String str = "911";
	- int i = Conver.ToInt32(str);
*/
```
### Singed vs Unsigned
```c#
/*
	> Unsigned means not negative values, it can hold a larger positive value
	> Signed can hold both positive and negative
*
```

## Class & Objects
```c#
/*
	> Class
		- A class is a blueprint, a tempplate
		- It has attributes & methods defined
	> Object
		- Object is a instance of a class
		- If we want to use a class we must create a instance of it
*
```

## Namespace
```c#
/*
	> Namespaces are used to group relative classes together
*
```

## Value & Reference types
```c#
/*
	> Value types:
		- Are copied and are stored in the stack
		- points to different address
		- example would be a int
		- static size

	> Reference types:
		- Are not copied and are stored in the heap
		- points to the same address
		- example would be a object
		- dynamic size
*/
```

## Garbage collection
```c#
/*
	> Handles the process of memory management
		- Clears out memory allocations that doesn't have reference
*/
```

## Stack Vs Heap
```c#
/*
	> Heap stores reference types
	> Stack stores value types & pointers of reference types
```

## Struct
[[C-sharp Notes#Struct]]
```c#
/*
	> Is a composite VALUE TYPE
		- Can have methods and variables
*/

```

## Boxing & Unboxing
```c#
/*
	> Boxing
		- converting a VALUE TYPE a REFERNECE TYPE
	> Unboxing
		- converting a REFERNCE TYPE to a VALUE TYPE
*
```

## Collections
[[C-sharp Notes#Collections]]
```c#
/*
	> ArrayList
		- Boxing occurs
	> List 
		- Is better no boxing happens but we must pass the data type
*
```

## Threading 
[[C-sharp Notes#Threading]]
```c#
/*
	> Threading is used when we want to run code parallelly
	> Runs on the same core (time slicing)

```

### Foreground Vs Background thread
```c#
/*      
	> Foreground Thread
		- A thread that is fully executed
	> Background Thread
		- A low priority thread that will get killed when all the foreground threads are fully executed.
*/
```

### Thread-safe
```c#
/*
	- Eliminates race conditions where two or more threads can access shared data
*
```

### Auto & Manual reset event
```c#
/*
	> Allows achieving sychnozation using signaling
	> Auto-reset
		 Turn style gate, one person can enter at a time
	> Manual-reset
		- Ordanary gate, everyone rush in
*/
```

### Thread pooling
```c#
/*
	> Reuses threads, rather than creating and destroying them each time
	> Performance gains
	> Can set a limit
*
```

## Task (TPL)
```c#
/*
	> Doesn't have thread affinity, where it tries to run in the same core
*/
```

## Async Await
[[C-sharp Notes#Async Await]]
```c#
/*
	> Eliminate default synchronous code where everything has to be done sequentially
		- calls back when await is done
		- Runs on the same thread
		- acts as a background thread but does not create a thread
*
```

## Delegate
[[C-sharp Notes#Delegate]]
```c#
/*
	> A pointer to a function
		- similar to a callback funtion
*
```
#### Multicast delegate
```c#
/*
	> Sends callbacks to multiple callers 
		- BI-DIRECTIONAL communication
*
```
### Event
```c#
/*
	> Sends callbacks to multiple callers 
		- UNI-DIRECTIONAL communication
*
```

## Anonymous function
```c#
/*
	> Function without a name
		- Usecase, only needs to be called once
*
```
### Lambda expression
```c#
/*
	> Is an inline function
*
```
### Func
```c#
/*
	> A type of delegate can declare inputs and outputs
*
```

### Action
```c#
/*
	> Same as a func but the return type is always void
*
```
### Predicate
```c#
/*
	> A type of delegate that can only return a boolean
*
```

## LINQ (Language integrated query)
```c#
/*
	> write (sql) queries inside .Net that can be execetued on:
		- xml
		- RDBMS
		- collentions
*
```

## Strings
```c#
/*
	> Strings are immutable(CAN NOT BE CHANGED)
		- It creates a new copy each time assigned
		- a = "bird"//new copy is created and old copy is GC'd
*/
```
### Interning
```c#
/*
	> If the string value is the same no copy is created
*
``` 

## Constants
```c#
/*
	> Constant variables can be only assigned once
		- Cannot be changed later
*/
```

### Enum
```c#
/*
	> A Enum is a group of related constants
*/
```
