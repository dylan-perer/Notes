## Initialization

->: https://start.spring.io/
1. configure name business name
2. add dependencies, spring web = rest API | h2 database = mockup DB for testing
3.  hit download

![[Screenshot 2022-02-21 164555.png]]

### Project Structure
```java
/*
  spring-demo/main/java/com/spring-demo.java = main
  spring-demo/pom.xml = all the dependecies
*/
```

### Changing default port
```properties
# got to: spring-demo/src/main/resources/application.properties

#run the app on this port
server.port = 8082
```

## Concepts
### M.V.C
```java
/*
	Model      -> The data, i.e packaged in a suitcase
	View       -> Showing the data to the user
	Controller -> Business logic, i.e. retrieve or update some data from the DB
*
```

### I.O.C
```java
/*
	Inversion of Control

	It is LETTING spring framework CREATE OBJECTS rather than our selfs
*
```

### Dependency Injection
```java
/*
	It is the process of INJECTING OBJECTS INTO OTHER OBJECTS, said that object has a dependency as the other object 
*
```


## Adding more dependencies
```xml
<!-- 1. https://start.spring.io/
   2. add new dependencies & copy them by clicking explore
   3. paste them in pom.xml then sync -->

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
    <scope>runtime</scope>
    <optional>true</optional>
</dependency>
```

## Live Reload
```java
/* for JIdea
1. add dev tools dependency in pom.xml & sync | failed to make it work :(
```

## Thymleaf (View Templates)
### Initialization
```xml
<!-- add thymleaf dependency to pom.xml -->
<dependency>  
   <groupId>org.springframework.boot</groupId>  
   <artifactId>spring-boot-starter-thymeleaf</artifactId>  
</dependency>
```

```java
/* Make a controller
   Create view templates in resources/templates/ -> index.html | index.html will default to / */

    package com.businessname.spring.demo.controller;  
	import org.springframework.stereotype.Controller;  
	import org.springframework.ui.Model;  
	import org.springframework.web.bind.annotation.GetMapping;  
	  
	@Controller  
	public class HomeController {  
	  
	 @RequestMapping("/") 
	 public String index(Model model){  
	        model.addAttribute("something", "this is coming form the controller");  
	        return "index";  
	    }  
	}
```

```html
<!DOCTYPE html>  
<html xmlns:th="http://www.thymeleaf.org">  
<head>  
    <meta charset="UTF-8">  
    <title>Title</title>  
</head>  
<body>  
    <h1 th:text="${something}"/>  
</body>  
</html>
```

### Show object in Thymleaf
```java
@GetMapping("/showPersonObject")  
public String showPersonObject(Model model){  
    Person person = new Person("Jhon",23);  
    model.addAttribute(person);  
    return "showPersonObjectHTML";  
}
```

```html
<body>  
	<h1 th:text="${person}"></h1>  <!--person is the object passed, default print toString()-->
	<h1 th:text="${person.name}"></h1>  <!-- person object attribute-->
</body>
```

### Tables 
```java
//Controller mapping to list
@GetMapping("/list")  
public String listPeople(Model model){  
    Person p1 = new Person("Jhon", 23);  
    Person p2 = new Person("Emma", 28);  
    Person p3 = new Person("Elise", 19);  
    Person p4 = new Person("Hannah", 43);  
  
    ArrayList<Person> people = new ArrayList<>();  
    people.add(p1);  
    people.add(p2);  
    people.add(p3);  
    people.add(p4);  
    model.addAttribute("peopleList", people);  
    return "peopleList";  
}
```

```html
<!--peopleList-->
<div th:each="person : ${peopleList}">  
    Name: <h4 th:text="${person.name}" />  
    Age: <h4 th:text="${person.age}" />  
</div>
```

### Conditionals
#### If else
```html
<td th:text="${teacher.active} ? 'ACTIVE' : 'RETIRED'" /> <!--ternary operation-->
```

#### Switch
```html
<div th:switch="${user.role}"> 
  <p th:case="'admin'">User is an administrator</p>
  <p th:case="#{roles.manager}">User is a manager</p>
  <p th:case="*">User is some other thing</p> 
</div>
```

### Get user input
@RequestParam 
```java
//shorter way of getting input from data

@RequestMapping("/processedForm")  
public String shoutName(@RequestParam("name") String name, Model model){  
    name = name.toUpperCase();  
  
    model.addAttribute("nameUppercase", "Your name in uppercase: "+name);  
    return "processedFormView";  
}
```


### Forms and validation
```java
//Create your MODEL
package com.businessname.spring.demo.model;  
import javax.validation.constraints.Min;  
import javax.validation.constraints.NotNull;  
import javax.validation.constraints.Size;  
  
public class Person {  
 /* Validation annotations can be combined! i.e    
 @Digits  
 @Positive */ 

    @NotNull  
	@Size(min=2, max=30)  
    private String name;  
  
    @NotNull  
    @Min(18)  
    private Integer age;  
  
    public String getName() {  
        return this.name;  
    }  
  
    public void setName(String name) {  
        this.name = name;  
    }  
  
    public Integer getAge() {  
        return age;  
    }  
  
    public void setAge(Integer age) {  
        this.age = age;  
    }  
  
    public String toString() {  
        return "Person(Name: " + this.name + ", Age: " + this.age + ")";  
    }  
}
```

```java
//create your CONTROLLER
package com.businessname.spring.demo.controller;  
import com.businessname.spring.demo.model.Person;  
import org.springframework.stereotype.Controller;  
import org.springframework.validation.BindingResult;  
import org.springframework.web.bind.annotation.GetMapping;  
import org.springframework.web.bind.annotation.PostMapping;  
import org.springframework.web.bind.annotation.RequestMapping;  
import org.springframework.web.servlet.config.annotation.ViewControllerRegistry;  
import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;  
import javax.validation.Valid;  
  
@Controller  
@RequestMapping("/person")  //Parent relative mapping
public class PersonController implements WebMvcConfigurer {  
        @Override  
		public void addViewControllers(ViewControllerRegistry registry) {  
            registry.addViewController("/results").setViewName("personFormResults");  //to path /results set view to personFormResults
        }  
  
        @GetMapping("/form")  
        public String showForm(Person person) {  
            return "personForm";  
        }  
  
        @PostMapping("/processForm")  
        public String checkPersonInfo(@Valid Person person, BindingResult bindingResult) {  
            if (bindingResult.hasErrors()) {  
                return "personForm";  
            }  
            return "redirect:/results";  //redirect to /results
        }  
}
```

```html
<!-- personForm-->
<!DOCTYPE HTML>  
<html xmlns:th="http://www.thymeleaf.org">  
<body>  
<form action="#" th:action="@{/person/processForm}" th:object="${person}" method="post"> 
  <table>  
    <tr>  
      <td>Name:</td>  
      <td><input type="text" th:field="*{name}" /></td>  
      <td th:if="${#fields.hasErrors('name')}" th:errors="*{name}">Name Error</td>  <!--if name field has errors show here-->
    </tr>  
    <tr>  
      <td>Age:</td>  
      <td><input type="text" th:field="*{age}" /></td>  
      <td th:if="${#fields.hasErrors('age')}" th:errors="*{age}">Age Error</td>  <!--if age field has errors show here-->
    </tr>  
    <tr>  
      <td><button type="submit">Submit</button></td>  
    </tr>  
  </table>  
</form>  
</body>  
</html>
```

```html
<!-- personFormResults-->
<html>  
	<body>  
		Congratulations! You are old enough to sign up for this site.  
	</body>  
</html>
```

### CSS
#### External CSS
```html
<!-- Springs default static folder is located at src/main/resources. make a folder -> css/demo.css* -->

<!DOCTYPE html>  
<html xmlns:th="http://www.thymeleaf.org">  
<head>  
    <meta charset="UTF-8">  
    <title>Title</title>  
	<!--reference CSS file -->
	<link rel="stylesheet" th:href="@{/css/demo.css}"/>
</head>  
<body>  
    <h1 th:text="${something}" class="header-red"/>  
</body>  
</html>
```


## Relative mapping
```java
@Controller  
@RequestMapping("/home")  // Home as this parent of all mappings in this class. i.e. /Home/showForm
public class HomeController {  
  
    @RequestMapping("/showForm")  
    public String showForm(){  
        return "uppercaseForm"; //name of view  
 }  
  
    @RequestMapping("/processedForm")  
    public String shoutName(@RequestParam("name") String name, Model model){  
        name = name.toUpperCase();  
  
        model.addAttribute("nameUppercase", "Your name in uppercase: "+name);  
        return "uppercaseFromProcess";  
    }  
}
```

```html
<!--index.html-->
<body>  
    <a href="/home/showForm">Name to Uppercase</a>  
</body>

<!--uppercaseForm-->
<form action="processedForm" method="GET">  
    <input type="text" name="name" placeholder="Enter your name"/>  
    <input type="submit"/>  
</form>

<!--uppercaseFromProcess-->
<body>  
    <h1 th:text="${nameUppercase}"/>  
</body>
```

## Validation
### Hibernator validation 
```xml
<!-- Add dependecy to pom.xml--> 
<dependency>
	 <groupId>org.springframework.boot</groupId>
	 <artifactId>spring-boot-starter-validation</artifactId>
 </dependency>
```



## Hibernate (O.R.M)
