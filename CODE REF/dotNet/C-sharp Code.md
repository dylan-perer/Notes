## Console
### Output
```c#
Console.WriteLine("Hello world");
```
### Read input 
``` c#
Console.Read();
```

## Data Types
```c#
string stringVar = "Hello World";
int intVar = 150;
float floatVar = 10.2f;
char charVar = 'E';
bool boolVar = false;
byte test = 255;

DateTime dateTimeVar = DateTime.Now;

Console.WriteLine($"{stringVar}, {intVar}, {floatVar}, {charVar}, {boolVar}, {dateTimeVar}, {test}");

Console.WriteLine(sizeof(int));//get the size of a date type
```

## Constants
```c#
class Program
{
    static void Main(string[] args)
    {
        const double pi = 3.14159;
        ClassA classA = new ClassA(pi);


    }
    private class ClassA
    {
        readonly double pi;
        const double x = 69.69;

        public ClassA(double pi)
        {
            this.pi = pi;//read-only variables can be assigned dynamically but it MUST be assigned before the constructor exits
        }

    }
}
```

## Random number
```c#
Random o = new Random();

int num = o.Next(1,2)// generate a number between 1 and 2
```
## Access Modifiers
### Protected
```c#
    public class Run
    {
        private class Animal
        {
            private protected int numOfLegs = 4;//adding private will only allow Run + classes that extends Animal to call it.
        }

        private class Cat: Animal
        {
            public int getNumOfLegs()
            {
                return numOfLegs;
            }

        }
        public static void Main(string[] args)
        {
            //protected members can onnly be accessed if the class calling that memeber is extended by it,
            //so super classes and abstracted classes
            Cat cat = new Cat();
            Console.WriteLine(cat.getNumOfLegs());
        }
    }
```
### Internal
```c#
/*
	Using an internal modifier will allow any class within the same assembly to access it
	protected internal will be  accessible anywhere is the same assembly and derived
*/
```

## Strings
### Formatting
```c#
string stringVar = "Hello World";
int intVar = 150;
float floatVar = 10.2f;
char charVar = 'E';
bool boolVar = false;
DateTime dateTimeVar = DateTime.Now;

Console.WriteLine($"{stringVar}, {intVar}, {floatVar}, {charVar}, {boolVar}, {dateTimeVar}"); //$"{variable} "
```

## Collections
```c#
int[] numArray = new int[3];
numArray[0] = 1;
numArray[1] = 2;
numArray[2] = 3;

foreach (int i in numArray)
{
	Console.WriteLine(i);
}

ArrayList arrayList = new ArrayList();// boxing happes
arrayList.Add(21);
arrayList.Add("apple");

List<int> list = new List<int>(); //no boxing
list.Add(21);
list.Add(100);
```

### LINQ (queries)
```c#
struct Person
{
	public string Name { get; set; }
	public int Age { get; set; }

	public Person(string Name,int Age)
	{
		this.Name = Name;
		this.Age = 0;   
	}
}
static void Main(string[] args)
{
	List<Person> people = new List<Person>();
	people.Add(new Person("Elise", 24));
	people.Add(new Person("Jhon", 18));
	people.Add(new Person("Susan", 54));
	people.Add(new Person("Tom", 32));

	List<Person> queryRes = (from person in people where person.Name.Length >=3 select person).ToList();
	foreach (Person person in queryRes)
	{
		Console.WriteLine(person.Name);
	}
}
```
## Struct
```c#
//can implement interfaces but cannot inherit
struct Student {
	public string name { get; set; }
	public int age { get; set; }

	public Student(string name, int age)
	{
		this.name = name;
		this.age = age;
	}

	public string toString() { 
		return $"{this.name} {this.age}";   
	}
}

static void Main(string[] args)
{
	Student student = new Student("Elise", 23);

	Console.WriteLine(student.toString());
}
```

## Enums
```c#
static void Main(string[] args)
{
	Console.WriteLine(WeekDays.Sunday);
	Console.WriteLine((int)WeekDays.Monday);
}

enum WeekDays
{
	Monday = 1, 
	Tuesday =2, 
	Wednesday=3, 
	Thursday=4, 
	Friday=5, 
	Saturday=6, 
	Sunday=7 
}
```

## Pass function as a parameter
```c#
public class AccessDemo
{
    public static void Main()
    {
        AccessDemoClass accessDemoClass = new AccessDemoClass();
        accessDemoClass.doSomething(functionToPass);
    }

    private static int functionToPass(string str, string str2)//function to be passed as a paramemter
    {
        //converts string int a int
        return int.Parse(str+str2);
    }
    class AccessDemoClass
    {
        internal void doSomething(Func<string, string, int> convert)//inputs ->... ->out
        {
            Console.WriteLine(convert("200", "1"));
        }
    }
}

```

## Threading
```c#
Thread t1 = new Thread(() => {
	for (int i = 0; i < 10; i++)
	{
		Console.WriteLine($"fun1: {i}");
	}
});
t1.IsBackground //will make the threa a background thread
t1.Start();

Console.WriteLine("done");//t0 main thread
```
### Threadsafe
```c#
Thread t1 = new Thread(() => {
	for (int i = 0; i < 10; i++)
	{
		lock(this){
			y = x / t; //secured code
		} 
	}
});
```
### Auto reset event
![[Screenshot 2022-03-07 021607.png]]

## Async Await
```c#
static void Main(string[] args)
{
	itterate();
	int x = 100;
	Console.ReadLine();
}

private static async void itterate()//async will die if the main thread dies
{
	for(int i = 0; i < 1000; i++)
	{
		await Task.Delay(1000);
		Console.WriteLine($"Async: {i}");
	}
}
```

## Files
```c#
File.WriteAllText(@"./data.txt", "some text");

string content = File.ReadAllText(@"./data.txt"); //@ will tell compiler to ignore escape characters
Console.WriteLine(content);
```

## Delegate
```c#
 static void Main(string[] args)
{
	Stream stream = new Stream();// set the pointer to print stream
	Task task = new Task(() => {
		stream.StreamTask(printStream);
	});

	task.Start();
	Console.ReadLine();
}

static void printStream(int i)
{
	Console.WriteLine(i);
}

class Stream
{
	public delegate void StreamDelegate(int i);//a delegate that takes a int and returns 

	public void StreamTask(StreamDelegate streamDelegateObject)
	{
		for(int i = 0; i < 100; i++)
		{
			Thread.Sleep(1000);
			streamDelegateObject(i);//calling the delegate
			
		}
	}

}
//for multicast delegate call streamDelegateObject(i); where u want it again and use += when assigning it
```

## TODO: in out ref
