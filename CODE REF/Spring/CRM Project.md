## CRM - demo
### Initialization
#### Pom.xml
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
#### MySQL config
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