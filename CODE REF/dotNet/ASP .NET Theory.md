## What is MVC core?
```c#
/*
	> A crossplatform web development framework.
*
```

## Explain MVC architecture
```c#
/*
	> Project is devided into three layers
		- Model (acts like a data suitcase)
		- View (what we show the the end user)
		- Controller (where we write the bussiness logic and bind models and views)
*
```

## What is 'wwwroot' folder
```c#
/*
	> It is where we store static contents.
*
```

## Explain the importance of 'appsettings.json'
```c#
/*
	> It is where all configuration data should go. i.e. connection string.
*
```

## How to read configurations from 'appsettings.json'
```c#
/*
	> By using IConfigration object.
*
```

## What is depedency Injection?
```c#
/*
	> Its allowing creation of object to be handled by mvc core.
	> Then it is injected to the class that needs that object
*
```

## Why do we need dependecy injection?
```c#
/*
	> We can have a decoupled system.
*
```

## How do you implemnt dependecy injection?
```c#
/*
	> In the starup file, inside configure services method we can define dependecy injection.
*
```

## What is the use of middleware?
```c#
/*
	> It is some pre-processing logic that is run before a request hit the controller.
*
```

## How to implement middleware?1
```c#
/*
	> In configure method inside startup.cs, we need to use app.use<middleware>
*
```

## What is 'startup.cs' file
```c#
/*
	> It is where middlewares and depedencny injections we want to use are configured.
*
```

## DIfference between 'configure ' and configureservices'
```c#
/*
	> configure, we declare middleware.
	> configureservices, we configure dependecies and their behaviour.
*
```

## Explain 'Scoped' dependency injection
```c#
/*
	> Injects a new instance per request.
*
```

## Explain 'Singleton' dependency injection
```c#
/*
	> Injects the same instace.
*
```

## Explain 'Transient' dependency injection
```c#
/*
	> Injects new instances every time.
*
```

## What is Razor?
```c#
/*
	> it is a View template engine.
	> Allows us to write server code and html in the same file.
*
```

## How to pass model to a view?
```c#
/*
	> return view with name and model.
*
```

## What are stongly typed views?
```c#
/*
	> A view with a type of the model bind to it.
*
```

## What is a view model?
```c#
/*
	> It is  a wrapper class that wraps around 2 or more models which is passed to the view.
*
```

## What is kestral?
```c#
/*
	> Default web server used by asp core.
	> When deploying krestal will act as a reverse proxy to another web server like nginx.
*
```

## Why not use IIS web server?
```c#
/*
	> Its windows only. 
*
```

## What are cookies?
```c#
/*
	> It a file with small bits of data stored in the end user's machine.
*
```

## What Session management?
```c#
/*
	> Since HTTP is stateless, we need sessions to keep track of the state. 
*
```

## What is http context
```c#
/*
	> It holds headers, session and request info.
*
```

## What is viewData and how should it be used?
```c#
/*
	> It is used to pass value from controller to view.
	> It will only persist for a single request.
*
```

## What is viewBag and how should it be used?
```c#
/*
	> It is sintatical sugar for viewData.
*
```

## Explain tempdata?
```c#
/*
	> We can decide when to dispose the data unlike view data
*
```

## Can tempdata persist from action to action and what is peek?
```c#
/*
	> It will persist till it is read.
	> we can use peek rathe than read to persist the value.
*
```

## Explain Session variables Vs ViewData vs TempData
```c#
/*
	> Session scope is from browser open to browser exist.
	> ViewData scope is form controller to a view.
	> TempData score is action to action till it is read.
*
```

## What is Web APi
```c#
/*
	> Remotely hosted functions over http protocol.
*
```

## What makes a RESTful Api
```c#
/*
	> REST is a set of guidelines that we can follow to make a web-API a RESTful API, such as 
		- Client-server
		- Stateless
		- Uniform Interface
		- Layered system
*
```

## Difference between MVC vs Web API controllers
```c#
/*
	> MVC controller returns a view.
	> API Controller retunrs a IActionResult, which can a json for example.
*
```

