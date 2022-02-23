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

## M.V.C
```java
/*
	Model      -> The data, i.e packaged in a suitcase
	View       -> Showing the data to the user
	Controller -> Business logic, i.e. retrieve or update some data from the DB
*
```

