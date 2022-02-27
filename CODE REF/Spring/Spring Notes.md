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

#### @Autowired
```java
public class customerDOAImpl implements customerDOA{
	//session factory in being injected to customerDOAImpl, i.e. sessionFactory is a dependecy of customerDOAImpl
	@Autowired
	private sessionFactory sessionFactory;

	public List<Customer> getCustomers(){..}
}
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

### Links
```html
<a th:href="@{/customerForm}">Add customer</a>
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

### Lists
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

<!-- as a table -->
<table>  
    <thead>  
        <tr>  
            <th>Name</th>  
            <th>Age</th>  
        </tr>  
    </thead>  
    <tbody>  
        <tr th:each="person: ${peopleList}">  
            <td th:text="${person.name}"></td>  
            <td th:text="${person.age}"></td>  
    </tbody>  
</table>
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
### Initialization
```xml
<!-- add dependencies to pom.xml-->
<dependency>
	 <groupId>org.springframework.boot</groupId>
	 <artifactId>spring-boot-starter-data-jpa</artifactId>
 </dependency>

 <dependency>
	 <groupId>org.springframework.boot</groupId>
	 <artifactId>spring-boot-starter-web</artifactId>
 </dependency>

 <dependency>
	 <groupId>mysql</groupId>
	 <artifactId>mysql-connector-java</artifactId>
	 <scope>runtime</scope>
 </dependency>
```

```xml
<!-- Configure DB-->
<!-- CREATE this XML file NAMED = hibernate.cfg in src/main/resources folder-->

<!DOCTYPE hibernate-configuration PUBLIC  
 "-//Hibernate/Hibernate Configuration DTD 3.0//EN"  
 "http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">  
<hibernate-configuration>  
    <session-factory>  
	 <!-- JDBC Database connection settings -->  
	 <property name="connection.driver_class">com.mysql.cj.jdbc.Driver</property>  
	        <property name="connection.url">jdbc:mysql://localhost:3306/hb_student_tracker?useSSL=false&amp;serverTimezone=UTC</property>  
	        <property name="connection.username">hbstudent</property>  
	        <property name="connection.password">hbstudent</property>  
	  
	 <!-- JDBC connection pool settings ... using built-in test pool -->  
	 <property name="connection.pool_size">1</property>  
	  
	 <!-- Select our SQL dialect -->  
	 <property name="dialect">org.hibernate.dialect.MySQLDialect</property>  
	  
	 <!-- Echo the SQL to stdout -->  
	 <property name="show_sql">true</property>  
	  
     <!-- Set the current session context -->  
	 <property name="current_session_context_class">thread</property>  
   
    </session-factory>  
</hibernate-configuration>
```

### Saving a object
```java
//Create entity
package com.businessname.spring.demo.entity;  
import javax.persistence.Column;  
import javax.persistence.Entity;  
import javax.persistence.Id;  
import javax.persistence.Table;  
  
@Entity //tell hibernate this is an entity  
@Table(name = "student") //the table we want to map this class to  
public class Student {  
    @Id  
	@GeneratedValue(strategy = GenerationType.IDENTITY)//Auto increment id
    @Column(name="id")  
    private int id;  
  
    @Column(name="first_name")  
    private String firstName;  
  
    @Column(name="last_name")  
    private String lastName;  
  
    @Column(name="email")  
    private String email;  
  
    public Student(){}  
  
    public Student(String firstName, String lastName, String email) {  
        this.firstName = firstName;  
        this.lastName = lastName;  
        this.email = email;  
    }  
  
    public int getId() {  
        return id;  
    }  
  
    public void setId(int id) {  
        this.id = id;  
    }  
  
    public String getFirstName() {  
        return firstName;  
    }  
  
    public void setFirstName(String firstName) {  
        this.firstName = firstName;  
    }  
  
    public String getLastName() {  
        return lastName;  
    }  
  
    public void setLastName(String lastName) {  
        this.lastName = lastName;  
    }  
  
    public String getEmail() {  
        return email;  
    }  
  
    public void setEmail(String email) {  
        this.email = email;  
    }  
  
    @Override  
 public String toString() {  
        return "Student{" +  
                "id=" + id +  
                ", firstName='" + firstName + '\'' +  
                ", lastName='" + lastName + '\'' +  
                ", email='" + email + '\'' +  
                '}';  
    }  
}
```

```java
package com.businessname.spring.demo.hibernatedemo;  
import com.businessname.spring.demo.entity.Student;  
import org.hibernate.Session;  
import org.hibernate.SessionFactory;  
import org.hibernate.cfg.Configuration;  
  
  
public class CreateStudentDemo {  
    public static void main(String[] args){  
        SessionFactory factory = new Configuration()//Create session factory  
				.configure("hibernate.cfg.xml")  
                .addAnnotatedClass(Student.class)  
                .buildSessionFactory();  
  
        Session session = factory.getCurrentSession();//create session  
  
 try {  
            Student student = new Student("Paul", "Wall", "paulw@gmail.com");  
            session.beginTransaction();  
            System.out.println("saving student to db...");  
            session.save(student);  
            session.getTransaction().commit();  
        }finally {  
            factory.close();  
        }  
    }  
}
```

## CRM - demo
### Initialization
```xml
<!-- DEPENDENCIES are MySQL driver, JPA, hibernate, spring web, Thymleaf | make SURE they are added to pom.xml-->
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>

<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-web</artifactId>
</dependency>

<dependency>
	<groupId>mysql</groupId>
	<artifactId>mysql-connector-java</artifactId>
	<scope>runtime</scope>
</dependency>
```

```properties
#run the app on this port  
server.port = 8082  
  
#DATASOURCE/DB Config  
spring.datasource.url=jdbc:mysql://localhost:3306/web_customer_tracker?useSSL=false&serverTimezone=UTC&useLegacyDatetimeCode=false  
spring.datasource.username=springstudent  
spring.datasource.password=springstudent  
  
#HIBERNATE Config  
spring.jpa.properties.hibernate.dialect = org.hibernate.dialect.MySQL5Dialect  
spring.jpa.hibernate.ddl-auto=update  
  
#Logging  
logging.level.org.hibernate.SQL = DEBUG  
logging.level.org.hibernate.type = TRACE
```

### Project Structure
![[Screenshot 2022-02-27 134536.png]]
#### Entity
```java
//Customer Entity
package com.example.mvc.model;  
import javax.persistence.*;  
  
@Entity  
@Table(name="customer")  
public class Customer {  
    @Id  
 @GeneratedValue(strategy = GenerationType.IDENTITY)//auto increments id  
 @Column(name="id")//make sure the column name is that same as in DB table.  
 private int id;  
  
    @Column(name="first_name")  
    private String firstName;  
  
    @Column(name="last_name")  
    private String lastName;  
  
    @Column(name="email")  
    private String email;  
  
    public int getId() {  
        return id;  
    }  
  
    public void setId(int id) {  
        this.id = id;  
    }  
  
    public String getFirstName() {  
        return firstName;  
    }  
  
    public void setFirstName(String firstName) {  
        this.firstName = firstName;  
    }  
  
    public String getLastName() {  
        return lastName;  
    }  
  
    public void setLastName(String lastName) {  
        this.lastName = lastName;  
    }  
  
    public String getEmail() {  
        return email;  
    }  
  
    public void setEmail(String email) {  
        this.email = email;  
    }  
}
```

#### Repository
```java
//REPOSITORY
//handles interfacing with a database to retrieve and store data | exposes CRUD operations  
package com.example.mvc.repository;  
import com.example.mvc.model.Customer;  
import org.springframework.data.jpa.repository.JpaRepository;  
import org.springframework.stereotype.Repository;  
  
@Repository
public interface I_CustomerRepository extends JpaRepository<Customer, Integer> {//Integer is the customer primary key  
}
```

#### Service
```java
//SERVICE interface
package com.example.mvc.service;  
import com.example.mvc.model.Customer;  
import java.util.List;  
  
public interface I_CustomerService {  
    List<Customer> getALlCustomers();  
  
    void saveCustomer(Customer customer);  
  
    Customer getCustomer(int id);  
  
    void deleteCustomer(int id);  
}
```

```java
//SERVICE
//wrapper to customer repository retrieve and store data
package com.example.mvc.service;
import com.example.mvc.model.Customer;
import com.example.mvc.repository.I_CustomerRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import java.util.List;
import java.util.Optional;

@Service
public class CustomerService implements I_CustomerService {
    @Autowired
    private I_CustomerRepository customerRepository;//injecting repo implementation dependency

    @Override
    public List<Customer> getALlCustomers() {//retrieve all customers
        return customerRepository.findAll();
    }

    @Override
    public void saveCustomer(Customer customer) {//save/insert a new customer
        this.customerRepository.save(customer);
    }

    @Override
    public Customer getCustomer(int id) {
        Optional<Customer> optional = customerRepository.findById(id);
        if(optional.isPresent()){
            return optional.get();
        }else{
            throw new RuntimeException(" Customer not found id::"+id);
        }
    }

    @Override
    public void deleteCustomer(int id) {
        customerRepository.deleteById(id);
    }
}

```

#### Controller
```java
//CONTROLLER
package com.example.mvc.controller;  
import com.example.mvc.model.Customer;  
import com.example.mvc.service.I_CustomerService;  
import org.springframework.beans.factory.annotation.Autowired;  
import org.springframework.stereotype.Controller;  
import org.springframework.ui.Model;  
import org.springframework.web.bind.annotation.*;  
  
@Controller
@RequestMapping("/customer")
public class CustomerController {
    @Autowired
    private I_CustomerService customerService; //injecting customerService implementation dependency

    //list all customers handler
    @GetMapping("/list")
    public String listCustomers(Model model){
        model.addAttribute("customers", customerService.getALlCustomers());
        return "customer-list";
    }

    //add new customer handlers
    @GetMapping("/newCustomerForm")
    public String addCustomer(Model model){
        Customer customer = new Customer();
        model.addAttribute("customer", customer);
        return "new-customer-form";
    }

    @PostMapping("/processNewCustomerForm")
    public String saveCustomer(@ModelAttribute("customer") Customer customer){
        customerService.saveCustomer(customer);
        return "redirect:/customer/list";
    }

    //update a customer
    @GetMapping("/customerFormUpdate/{id}")
    public String showFormForUpdate(@PathVariable (value = "id") int id, Model model){
        //get customer
        Customer customer = customerService.getCustomer(id);

        //populate form
        model.addAttribute("customer", customer);
        return "update-customer-form";
    }

    @GetMapping("/deleteCustomer/{id}")
    public String deleteCustomer(@PathVariable (value = "id") int id){
        customerService.deleteCustomer(id);
        return "redirect:/customer/list";
    }

}
```

#### Views
```xml
<!--customer-list-->
<body>  
<button><a th:href="@{/customer/newCustomerForm}">Add customer</a></button><br>  
    <table>  
        <thead>  
            <tr>  
                <th>Id</th>  
                <th>First Name</th>  
                <th>Last Name</th>  
                <th>e-mail</th>  
                <th>Actions</th>  
            </tr>  
        </thead>  
        <tbody>  
            <tr th:each="customer: ${customers}">  
                <td th:text="${customer.id}"></td>  
                <td th:text="${customer.firstName}"></td>  
                <td th:text="${customer.lastName}"></td>  
                <td th:text="${customer.email}"></td>  
                <td><a th:href="@{/customer/customerFormUpdate/{id}(id=${customer.id})}">Update</a>  
                    <a th:href="@{/customer/deleteCustomer/{id}(id=${customer.id})}">Delete</a>  
                </td>  
        </tbody>  
    </table>  
</body>
```

```xml
<!--new-customer-form-->
<body>
    <h1>Add new customer</h1>
    <form action="#" th:action="@{/customer/processNewCustomerForm}" th:object="${customer}" method="POST">
        <input type="text" th:field="*{firstName}" placeholder="First Name">
        <input type="text" th:field="*{lastName}" placeholder="Last Name">
        <input type="text" th:field="*{email}" placeholder="e-mail">

        <input type="submit" value="Save customer">
    </form>
</body>
```

```xml
<!--update-customer-form-->
<body>
<h1>Update customer</h1>
<form action="#" th:action="@{/customer/processNewCustomerForm}" th:object="${customer}" method="POST">
    <input type="hidden" th:field="*{id}"><!-- hidden field to handle update-->
    <input type="text" th:field="*{firstName}" placeholder="First Name">
    <input type="text" th:field="*{lastName}" placeholder="Last Name">
    <input type="text" th:field="*{email}" placeholder="e-mail">

    <input type="submit" value="Add customer">
</form>
</body>
```

## AOP : TODO

## Maven: TODO

## Spring Security: TODO

## REST API - demo: TODO
