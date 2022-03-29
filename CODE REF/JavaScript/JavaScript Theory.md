## Why is js called a dynamic language?
```c#
/*
	> Because the data type of a variable can change during runtime.
*
```

## How does javascript determine data types?
```c#
/*
	> It assignes data types depending on the value assigned.
*
```

## What is typeof()?
```c#
/*
	> It returns a variable's data type.
*
```

## What is 'undefined'?
```c#
/*
	>  Variable was declared but no value was assigned.
*
```

## What is 'null'?
```c#
/*
	> Absance of data.
*
```

## Explain hoisting
```c#
/*
	> Varibles and function delarations are moved to the top of the scope before execution.
*
```

## Explain global variables
```c#
/*
	> A type of variable the can be accessed throughut the program.
*
```

## Cons of global variables?
```c#
/*
	> Makes code hard to debug.
	> Makes core more prone to bugs.
*
```

## How to declare a gloabal?
```c#
/*
	> without using var, let or const. just the varible name.
*
```

## What is 'use strict' ?
```c#
/*
	> Won't let you use varibles without declaration.
*
```

## What are closures?
```c#
/*
	> A funtion with state (function inside a function).
*
```

## Why do we need closures?
```c#
/*
	> To moularise and self contain.
*
```

## Explain 'IIFE'
```c#
/*
	> Anonymouse function that is imdediatly invoked.
*
```

## Use of 'IIFE'
```c#
/*
	> Name collison won't occur.
*
```

## What is module pattern
```c#
/*
	> Self contained components.
	> Provides Encapsulation and abstarction.
*
```

## What are the way to define variables is JS?
```c#
/*
	> literal
	> Object.create()
	> Constructor
*
```

## Explain inheritance in JS
```c#
/*
	> We use 'prototype' to delacre inheritance.
	> It's based on object inheritance rather than class inheritance.
*
```

## What is 'prototype' is JS
```c#
/*
	> Every object in JS has a prototype property. 
	> It the property used to declare inheritance.
*
```

## Explain 'let'
```c#
/*
	> Let is local scoped. 
*
```

## Are 'let' variables hoisted?
```c#
/*
	> Yes, but will not be initialized.
*
```

## Explain temporal dead zone?
```c#
/*
	> its a state of a variable where it is named in the memory but not initalized with value.
*
```

## JIT
```c#
/*
	> Compiles code in machine code when some code need to be executed.
*
```

## Explain call stack
```c#
/*
	> first in last out, 
	> Everything get pushed to the call stack then is poped off when that code is executed.
*
```

## Explain task queue
```c#
/*
	> Asnc code is pushed in to the task queue, not call stack.
	> When call stack is emptied and asyc code is fully executed it will be push into the call stack.
*
```

##  Explain Microtasks Queue
```js
/*
	> microtask queue is emptied/exhausted before task queue.
	> Promises are placed on the microtask queue

```
