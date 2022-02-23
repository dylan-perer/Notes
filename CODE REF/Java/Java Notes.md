# ::: Basics :::

## How java is RUN

![[Screenshot 2022-02-15 174800.png]]

![[Screenshot 2022-02-15 175320.png]]

## Data Types

````java
/* Primitive vs Reference
 Primitive data type has a SET SIZE i.e. booleans, int | stores data | faster
 Reference data types has UNLIMITED SIZE i.e string/objects | stores addresses | slower */ 
````

## String Concatenation

````java
float x = 3.56f;
System.out.print("This is my flaot "+x);
````

## Getting Input

````java
import java.util.Scanner;

public class Main {
	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
		
		//Get a string as input
		System.out.print("Enter string: ");
		String stringOutput = scanner.nextLine();
		
		//Get a int as input
		System.out.print("Enter int: ");
		int intOutput = scanner.nextInt();

		//nextInt() will just get the int and leave \n in the buffer, so we need to clear it
		scanner.nextLine();
		
		//Get a string as input
		System.out.print("Enter string: ");
		String stringOutput2 = scanner.nextLine();
		
		System.out.println("You typed: "+stringOutput);
		System.out.println("You typed: "+intOutput);
		System.out.println("You typed: "+stringOutput2);
	}
}				
````

## Math Class

````java
public class Main {
	public static void main(String[] args) {
		float x=4.93f, y =5.43f;
		//casting float x to a double
		System.out.println("max is "+Math.max((double)x, y));
		y*=-1;
		System.out.println("abs is "+Math.abs(y));
		System.out.println("squar-root is "+Math.sqrt(x));
	}
}
````

## Random Numbers

```java
import java.util.Random;

public class main {
    public static void main(String[] args){
        Random random = new Random();

        //Generate number between 1 and 6
        int x = random.nextInt(6)+1;
        System.out.println(x);

        //Generate number between 2 numbers
        int high=4, low=-4;
        int result = random.nextInt(high-low) + low;
        System.out.println(result);
    }
}
```

## Conditionals

### If Statement

```java
public class main {
    public static void main(String[] args){
        int age = 79;
        if(age >=75){
            System.out.println("okay boomer!");
        }else if(age >= 18){
            System.out.println("You are an adult!");
        }else{
            System.out.println("Go away kid");
        }
    }
}
```

### Switch

````java
public class main {
    public static void main(String[] args){
        String day = "Friday";
        switch (day){
            case "Monday":
                System.out.println("Its Monday");
                break;
            case "Friday":
                System.out.println("its Friday");
                break;
            default:
                System.out.println("No idea!!");
        }
    }
}
````

### Ternary Operator

````java
public class main {
    public static void main(String[] args){
        String day = "Friday";

        String today = day.equals("Friday")? day: "Today is not friday";
        System.out.println(today);
    }
}
````

## Loops

### For Loop

```java
public class main {
    public static void main(String[] args){
        String thisString = "This is a string";
        
        //for loop
        for (int i = 0;i<thisString.length();i++){
            System.out.println(thisString.charAt(i));
        }
    }
}
```

### While Loop & Do While

````java
public class main {
    public static void main(String[] args){
        String thisString = "This is a string";   
        
		//While loop
        int count = 0;
        while (count!=thisString.length()){
            System.out.println(thisString.charAt(count));
            count++;
        }

        //Do while
        count = 0;
        do{
            System.out.println(thisString.charAt(count));
            count++;
        }while (count!=thisString.length());
    }
}
````

### Foreach Loop

````java
public class main {
    public static void main(String[] args) {
        String [] animals = {"cat", "rat", "bird"};

        for(String i: animals){
            System.out.println(i);
        }
    }
}
````



## Arrays

````java
import java.util.ArrayList;

public class main {
    public static void main(String[] args){
        //Arrays
        String[] cars = {"Camaro", "Corvette", "Tesla"};
        System.out.println(cars[1]);

        //Initialize array without values
        String[] streets = new String[3];
        streets[0] = "st1";
        streets[1] = "st1";
        streets[2] = "st1";

        //Array Lists
        ArrayList<String> carsArrayList = new ArrayList<>();
        carsArrayList.add("car1");
        carsArrayList.add("car2");
        carsArrayList.add("car3");

        System.out.println(carsArrayList);
    }
}
````

### 2D Arrays

```java
public class main {
    public static void main(String[] args) {
        //2D arrays are array of array
        String [][] cars = new String[3][3];

        cars[0][0] = "car00";
        cars[0][1] = "car01";
        cars[1][0] = "car10";
        cars[1][1] = "car11";

        //Print out 2D array
        for (int i =0; i< cars.length; i++){
            for(int j = 0; j< cars[i].length; j++){
                if(cars[i][j]!=null){
                    System.out.println(i+","+j+":"+cars[i][j]);
                }
            }
        }
        //Initialize 2D Array in one line, row1, row2
        String[][] cars2 = {{"camaro","Corvette","silverado"},{"mustang","f150","Ranger"}};
    }
}
```

## Wrapper Classes

```java
public class main {
    public static void main(String[] args) {
        // This primitive doesn't have any other functionality | it is faster
        double x = 4.65;

        //This is a wrapper class, This primitive data type is now a Reference data type | slower but has more functionality
        Double xx = new Double(4.67);

        //i.e.
        System.out.println(xx.compareTo(x));
    }
}
```

### Autoboxing & Unboxing

````java
       //Autoboxing | Converting primitive type to reference | Unboxing is the opposite
        Double c = 4.34;
        Boolean b = true;
````

## Methods

````java
public class main {
    public static void main(String[] args) {
        System.out.println(add(2,3));
    }

    //static methods only can call other static methods, because we are calling this from main we need to have static
    static int add(int x, int y){
        return x+y;
    }
}
````

### Overloading

````java
    //overloading = method name + parameter = method signature
    static int add(int x, int y){
        return x+y;
    }

    static int add(int x, int y, int c){
        return x+y+c;
    }
````

## String formatting

````java
public class main {
    public static void main(String[] args) {

        boolean b = true;
        char c = '@';
        String str = "STRING";
        int i = 66;
        double d = 123.34;

        System.out.printf("a bool %b, a character %c, a string %s, a integer %d, a double %f", b, c, str, i, d);
    }
}
````

### Decimal points

````java
double d = 123.34343;
//2 decimals
System.out.printf("2 decimal %.2f",d);
````

## Constants

````java
//Use final keyword to make variables constant
final double PI= 3.143;
````

# ::: Intermediate :::

## Class

````java
public class main {
    public static void main(String[] args) {
        // creating a object from the class in main
        Human hum1 = new Human("dave", 28);
        System.out.println(hum1);
    }

}

class Human {
    private String name;
    private int age;

    //constructor
    public Human(String name, int age){
        this.name = name;
        this.age = age;
    }

    @Override
    public String toString() {
        return "Human{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}
````

## Static Keyword Modifier

````java
public class main {
    public static void main(String[] args) {
        Friend f1 = new Friend("Spongebob");
        Friend f2 = new Friend("Patrick");
        Friend f3 = new Friend("Squidward");

        System.out.println(Friend.numFriends); //static fields can be accessed directly
    }
}

class Friend{
    static int numFriends; //static field shared across all its objects
    private String name;

    public Friend(String name){
        this.name = name;
        numFriends++;
    }
}
````

## Inheritance

````java
public class main {
    public static void main(String[] args) {
        Car car = new Car();
        Bike bike = new Bike();
        
        car.go();
        bike.stop();
    }
}
// Car & Bike inherits from Vehicle | Vehicle is super class
class Vehicle{
    void go(){
        System.out.println("going..");
    }

    void stop(){
        System.out.println("stopping..");
    }
}

class Car extends Vehicle{
    int numWheels = 4;
}

class Bike extends Vehicle{
    int numWheels = 2;
}
````

## Method Overriding

```java
class Car extends Vehicle{
    int numWheels = 4;

    //Overriding super class (Vehicle class) go method
    @Override
    void go() {
        System.out.println("the car is going");
    }
}
```

## Super keyword

````java
class Person{
    String name = "Dave";
}

class Hero extends Person{
    String power;
    Hero(String power){
        //this = the class ur in | super refers to its parent class
        this.power = power;
        System.out.println("Hero name is "+super.name);
    }
}
````

## Abstract Class

```java
abstract class Vehicle{
    String color = "RED";
    abstract void go();
}
//Forces sub class to imlement
class Car extends Vehicle{
    @Override
    void go() {
        System.out.println(super.color+" Car is going...");
    }
}
```

## Access Modifiers

```java
/* No modifer = all classes in the same package has access
   public = access to classes in other packages
   protected = only accessable if its inherited even to other package classes
   private = only accessable to its own class
   
```

## Encapsulation

```java
class Car{
    // Variables are hidden
    private String make;
    private String model;
    private int year;
    
    Car(String make, String model, int year){
        this.setMake(make);
        this.setModel(model);
        this.setYear(year);
    }
	
    //public setters and getters
    public String getMake() {
        return make;
    }

    public void setMake(String make) {
        this.make = make;
    }

    public String getModel() {
        return model;
    }

    public void setModel(String model) {
        this.model = model;
    }

    public int getYear() {
        return year;
    }

    public void setYear(int year) {
        this.year = year;
    }
}
```

## Memory address of an Object

````java
Car car = new Car("Toyota", "Supra", 1994);
System.out.println(car.getAddress());

// by default ToString returns the address, since toString is overridden we can call super 
public String getAddress(){
    return super.toString();
}
````

## Copying Objects

````java
Car car = new Car("Toyota", "Supra", 1994);
Car car2 = new Car("Nissan", "SkyLine", 1997);

//if we do this it will just point ca2's address to car | DON'T DO THIS IF YOU WANT TO COPY
// car = car2;

car.copy(car2);

// copy method of Car
public void copy(Car x){
    this.setMake(x.getMake());
    this.setModel(x.getModel());
    this.setYear(x.getYear());
}
````

## Interface

````java
interface Prey{
    void eat();
}

interface Predator{
    void hunt();
}

// forces classes to implement interface methods
class Eagle implements Predator{
    @Override
    public void hunt() {
        System.out.println("Swoop down");
    }
}

class Rabbit implements Prey{
    @Override
    public void eat() {
        System.out.println("Eat");
    }
}
````

## Polymorphism

````java
public class main {
    public static void main(String[] args) {
        Animal animal1 = new Eagle();
        Animal animal2 = new Rabbit();
        
        // Because Animal is super of both Eagle & Rabbit we can polymorph them.
        Animal[] animals = {animal1, animal2};
        
        // Dynamic Polymorp happen in runtime. i.e. polymorph animal1 to Eagle if user input 1 else rabbit
    }
}

class Animal{
}

class Eagle extends Animal{
}
class Rabbit extends Animal{
}
````

## Try Catch

````java
public class main {
    public static void main(String[] args) {

        int x= 0;
        int y = 5;
        
	    // cant divide by 0
        try {
            int a=y/x;
            System.out.println(a);
        }catch (Exception e){
            // e = the type of exception
            System.out.println(e);
        }finally {
            System.out.println("This will always print");
        }
    }
}
````

## Regex

````java
public class main {
    public static void main(String[] args) {
        String text = "working today is it?";

        //Splitting | u can also add a limit after regex pattern to split by
        String[] textSplit = text.split("\s+");
        System.out.println(Arrays.toString(textSplit));

        //Replacing
        text=text.replaceAll("today","");
        System.out.println(text);

    }
}
````



# ::: Advanced :::

## File Class

```java
import java.io.File;

public class main {
    public static void main(String[] args) {
        // if file is in the project folder otherwise pass full path as G:/Downloads/secret.txt
        File file = new File("secret.txt");

        if(file.exists()){ // check if file exists
            System.out.println("File Exists");
            System.out.println(file.getPath());
            System.out.println(file.getAbsolutePath());
            file.delete();
        }else{
            System.out.println("nope");
        }
    }
}
```

### Read & Write File

```java
import java.io.*;

public class main {
    public static void main(String[] args) throws IOException {
        // writing to a file
        FileWriter writer = null;
        try{
            writer = new FileWriter("poem.txt");
            writer.write("Roses are red");
            writer.append("\npoem by Dylan");
        }catch (IOException e){
            e.printStackTrace();
        }finally {
            writer.close();
        }
		
        // reading to a file
        FileReader reader = null;
        try{
            reader= new FileReader("poem.txt");
            int data = reader.read();
            while (data!= -1){
                System.out.print((char) data);
                data = reader.read();
            }
        }catch (IOException e){
            e.printStackTrace();
        } finally {
            reader.close();
        }

    }
}
```

## Generics

### Generic Methods

```java
public class main {
    public static void main(String[] args) {
        Integer[] intArray = {4, 5, 56, 2, -4};
        Character[] charArray = {'c', 'w', 's', 't'};

        printArray(intArray);
        printArray(charArray);
        System.out.println(printArray(intArray)[0]);
    }
    // Thing become the type | it can be an integer character or any data type array
    // Inputs Thing[] and returns Thing[]
    static <Thing>Thing[] printArray(Thing[] array){
        for(Thing x: array){
            System.out.println(x+" ");
        }
        System.out.println();
        return array;
    }
}
```

### Generic Class

```java
public class main {
    public static void main(String[] args) {
        MyGenericClass<Integer> intGen = new MyGenericClass<>(4);
        MyGenericClass<Character> charGen = new MyGenericClass<>('c');
        System.out.println(intGen);
        System.out.println(charGen);

    }
	
    // You can have more than one generic type, i.e. <Thing, Thing2>
    private static class MyGenericClass<Thing>{
        Thing x;

        MyGenericClass(Thing x){
            this.x = x;
        }

        @Override
        public String toString() {
            return ""+x;
        }
    }
}
```

## Timer

### One-time execution

```java
import java.util.Timer;
import java.util.TimerTask;

public class main {
    public static void main(String[] args) {
        //Timer = A thread that keeps time
        //TimerTask = A task that can be scheduled for one-time or repeated execution

        Timer timer = new Timer();
        TimerTask task = new TimerTask() {
            @Override
            public void run() {
                System.out.println("Task is complete");
                //timer.cancel() // to cancel repeated execution
            }
        };

        //One time execution
        timer.schedule(task, 2000); // delay in ms
    }
}
```

### Repeated execution

```java
timer.scheduleAtFixedRate(task, 0, 1000); //task class, initial delay, period
//timer.cancel() on run method to cancell
```

## Threads

### Util functions

````java
public class main {
    public static void main(String[] args) throws InterruptedException {
        System.out.println(Thread.activeCount()); // show count
        System.out.println(Thread.currentThread().getName()); // show name
		
        // Thread priority is inherited, if main has 5 then thread created by it will also have 5
        System.out.println(Thread.currentThread().getPriority()); // 1 to 10, higher the number higher the priority
        Thread.currentThread().setPriority(10);

        Thread.currentThread().isAlive();// Check if still running

        for(int i = 0;i<10;i++){
            System.out.println(i);
            Thread.sleep(1000); // sleep pauses the thread
        }
    }
}
````

### Creating a new Thread

`````java

public class main {
    public static void main(String[] args) {
        MyThread t = new MyThread();
        t.start(); //don't use run()

        System.out.println(t.isAlive());
    }

    public static class MyThread extends Thread{
        @Override
        public void run() {
            while (true){
                System.out.println("This thread is running.,");
                try {
                    Thread.sleep(1000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
`````

### Daemon Threads

```java
// Daemon threads are low priority
// Java will quit even if daemon thread is running on teh background as long as all the user created threads finished their execution
MyThread t = new MyThread();
t.setDaemon(true);
t.start(); //don't use run()
```

## HTTP Connections

````java
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;

public class main {
    public static void main(String[] args) {
        HttpClient httpClient = HttpClient.newHttpClient();
        String API_ENDPOINT = "https://jsonplaceholder.typicode.com/albums";
        HttpRequest  httpRequest = HttpRequest.newBuilder().uri(URI.create(API_ENDPOINT)).build();

        //send request
        httpClient.sendAsync(httpRequest, HttpResponse.BodyHandlers.ofString())//return response body as a string
                .thenApply(HttpResponse::body)
                .thenAccept(System.out::println)
                .join();
    }
}
````



## Commandline compilation

```java
// Make sure Java JDK is installed
// Open cmd / terminal
// set path = (jdk/bin)
// cd to java file

// javac HelloWorld.java (to compile & generate byte code)
// HelloWorld.class = bytecode

// java HelloWorld (to run program)
```

#### Creating Executable

































