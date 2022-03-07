## Dependencies
```xml
<!--
	spring web: for REST API
	Lombok: Annotations for getters/setters/constructors/hash
	spring security: for authentication
	spring data: ORM
	mysql driver: connection to db
	java mail sender: to handle mail to users
	validation: to validate inputs
-->
```
### pom.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.6.4</version>
		<relativePath/> <!-- lookup parent from repository -->
	</parent>
	<groupId>com.nz</groupId>
	<artifactId>codex</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<name>codex</name>
	<description>codex</description>
	<properties>
		<java.version>11</java.version>
	</properties>
	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-data-jpa</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-mail</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-security</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-devtools</artifactId>
			<scope>runtime</scope>
			<optional>true</optional>
		</dependency>
		<dependency>
			<groupId>mysql</groupId>
			<artifactId>mysql-connector-java</artifactId>
			<scope>runtime</scope>
		</dependency>
		<dependency>
			<groupId>org.projectlombok</groupId>
			<artifactId>lombok</artifactId>
			<optional>true</optional>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
		<dependency>
			<groupId>org.springframework.security</groupId>
			<artifactId>spring-security-test</artifactId>
			<scope>test</scope>
		</dependency>
		<dependency>
		  <groupId>org.springframework.boot</groupId>
		  <artifactId>spring-boot-starter-validation</artifactId>
	    </dependency>
	</dependencies>

	<build>
		<plugins>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
				<configuration>
					<excludes>
						<exclude>
							<groupId>org.projectlombok</groupId>
							<artifactId>lombok</artifactId>
						</exclude>
					</excludes>
				</configuration>
			</plugin>
		</plugins>
	</build>

</project>

```

## Create the models
```java
/*  There are you entities
	Add @Entity
	Constructors, getters, setters, builders with Lombok (@Data, @AllArgsConstructor etc..)
	State the table relationships (@ManyToOne ...)
	Add Validation

*/

//Here is a example
package com.nz.codex.model;  
  
import lombok.AllArgsConstructor;  
import lombok.Builder;  
import lombok.Data;  
import lombok.NoArgsConstructor;  
import java.time.Instant;  
import static javax.persistence.FetchType.LAZY;  
import javax.persistence.*;  
import javax.validation.constraints.NotNull;  
  
@Data//Lombok helper annotations to create getters, setters, constructors on runtime  
@Builder  
@AllArgsConstructor  
@NoArgsConstructor  
@Entity//this is an entity  
public class Post {  
    @Id  
 @GeneratedValue(strategy = GenerationType.IDENTITY)  
    private long postId;  
  
    @NotNull(message = "Post title cannot be null")//validation error  
 private String title;  
  
    private String url;  
  
    @Lob//large chunk of text can be stored  
 private String description;  
  
    private int postVoteCount = 0;  
  
    @ManyToOne(fetch = LAZY)  
    @JoinColumn(name = "userId", referencedColumnName = "userId")//foreign key relationship  
 private User user;  
  
    private Instant createdDate;//date time datatype  
  
 @ManyToOne(fetch = LAZY)  
    @JoinColumn(name = "id", referencedColumnName = "id")//foreign key relationship  
 private Subreddit subreddit;  
  
}

```
## Create the repositories

```java
/*
	Repositories are what interface with the database
	there are INTERFACES!
	It is where all the DB queries are defined
*/

//Here is a example
package com.nz.codex.repository;  
  
import com.nz.codex.model.Post;  
import com.nz.codex.model.Subreddit;  
import com.nz.codex.model.User;  
import org.springframework.data.jpa.repository.JpaRepository;  
import org.springframework.stereotype.Repository;  
import java.util.List;  
  
@Repository  
public interface PostRepository extends JpaRepository<Post, Long> {  
    List<Post> findAllBySubreddit(Subreddit subreddit);  
  
    List<Post> findByUser(User user);  
}
```