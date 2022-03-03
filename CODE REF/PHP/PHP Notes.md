## Initialization
```php
this is treated as just text
<?php echo 'hello world'; // php comment  ?>
```
### Display errors
```php
//turn on display_errors = On in php.ini-development file
```

### Printing
```php
echo 'echo something';
print("print something\n");// slower that echo

$myVar = [342.34, 223, 304, "dog"];
print_r($myVar);
```


## Variables
```php
$myName = 'Dylan';//this is a variable in php

const USERNAME = 'Dyalan232' //constant variable

echo USERNAME;//notice u don't need to use $ with constant variables
```
### Embedding variables into html
```php
<?php 
    $para = "my title";
?>
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Document</title>
</head>
<body>
    <p><?=$para?></p>
</body>
</html>
```
## Strings
### Methods 
```php
$str = 'this is text';
strlen($str); //get string length
```
### Formatting
```php
$myName = 'Dylan';

echo 'hello '.$myName;
echo "hello, $myName";
```

## Conditionals
```php
$first_name = 'Elise';

if($first_name == 'Dylan'){
	echo 'name is '.$first_name;
}else if ($first_name == 'Elise'){
	echo 'hello! Elise';
}else{
	echo 'wassup guest!';
}
```

### Ternary operator
```php
$marks = 68;
echo ($marks>=40) ? "pass" : "Fail";
```
## Arrays
```php
$guitars = ['Vela', 'Explorer', 'Strat']; //not stricly typed so, [23, "cat", [2,3,1], 232.3]
echo $guitars[1];

if(isset($guitars[3])){//check if index exsist in array
	echo $guitars[3];
}else{
	echo "\nGuitar does not exist";
}

echo implode(" ", $guitars);// array to string
print_r($guitars)

array_map("get_element",$array);//map array

function get_element($item){//function to pass
	echo $item;
}
```
### Array methods
```php
$array = [32,2,3,-4];
array_pop($array);//remove last elem
array_push($array, "ham", "cheese");
array_splice($array, 2, count($array));//remove elements, start, end

print_r($array);
```
### Key pairs
```php
$cars = [
	'key1' => 'key1Val',
	'key2' => [2,3,4, 'bird'],
	'key3' => 23.23,
	'key4' => 'key4Val',
];

print_r($cars);
echo '<br>';

echo $cars['key3'];//getting value by passing key
```

## Loops
### For 
```php
for($i = 0; $i<10; $i++){
	echo $i;
}
```

### For each
```php
$guitars = [
	'prs' => 'vela',
	'sea' => 'nua',
	'gibson' => 'era'
];

foreach ($guitars as $key => $guitar) {
	echo "<br>$guitar<br>";
}
```

### While 
```php
$x = 5;
while($x>=0){
	$x--;
	echo "<br>$x<br>";
}
```

## Functions
```php
<?php
	function add($x, $y){
		return $x + $y;
	}
	
	echo add(24,-3);

	//using global variables
	$temp1 = 6;
	$temp2 = 5;
	
	function addWithGlobals(){
	    global $temp1, $temp2;
	    return $temp1+ $temp2;
	}
	
	echo addWithGlobals();
?>

<p><?=add(4,3)?></p><!-- call inside HTML -->
```
## Include & Require
```php
include('./inc/header.inc.php');//include the header file 
require('./functions/some.func.php')//fatal error returned | file must exsit!
require_once('./functions/some.func.php')//only executed once 
```


## Get request
### Query stream
```php
/*  https://www.google.com/search?client=firefox-b-d&q=php
	1. everything after the question mark are query parameters
	2. They are key-value pairs
*/

// GET localhost:3000/index.php?productId=10&limit=2

$product_id = $_GET['productId']; //$_GET is a super global and a array

echo "$product_id<br>"; //use isset() to error handle
echo $_GET['limit'];

//validate query params;
//INPUT_GET  because it is GET request, name of the query param, Data type we are expecting (int).
$product_id = filter_input(INPUT_GET,'productId', FILTER_VALIDATE_INT);//return false if fails or the value, on passed validation check
if ($product_id){
	//proceed
    echo $product_id;
}else{
	die();//execute no farther
}
````

## Redirect
```php
header('Location: admin.php');//redirect
```
## Post request
```php
<?php
if ($_SERVER['REQUEST_METHOD'] == 'POST') { //check if it's a POST request
    $email = filter_input(INPUT_POST, 'email', FILTER_VALIDATE_EMAIL);
    $password = $_POST['password'];
}
?>

<body>
    <form action="login.php" method="post">
        <label for="email">e-mail</label>
        <input type="email" name="email" id="email">

        <label for="password">password</label>
        <input type="password" name="password" id="password">

        <input type="submit" value="login">
    </form>
</body>

</html>
```

## Session
```php
<?php
//:: login.php ::
include('./config.php');
session_start();//use it in every file u want to use session variables


if ($_SERVER['REQUEST_METHOD'] == 'POST') { //check if it's a POST request
    $email = filter_input(INPUT_POST, 'email', FILTER_VALIDATE_EMAIL);
    $password = $_POST['password'];

    //check with store
    if(authenticate($email, $password)){
        $_SESSION['email'] = $email;
        header('Location: admin.php');//redirect
    }

}

function authenticate($email, $password){
    return $email == USER_NAME && $password == PASSWORD;        
}
?>

<body>
    <form action="login.php" method="post">
        <label for="email">e-mail</label>
        <input type="email" name="email" id="email">

        <label for="password">password</label>
        <input type="password" name="password" id="password">

        <input type="submit" value="login">
    </form>
</body>
</html>
```

```php
<?php
//:: config.php ::
const USER_NAME = "admin@admin.com";
const PASSWORD = "12345";
```

```php
<?php 
//:: admin.php ::
    session_start();
    print_r($_SESSION);
?>
```
### Destroy session
```php
//logging out
session_start();
session_unset();
session_destroy();

//redirect
```

## Classes
```php
class Person{
	public $firstName;//modifiers = public, private protected
	private $lastName;
	private $gender;

	public function __construct($firstName, $lastName,$gender='f'){
		$this->firstName = $firstName;
		$this->lastName = $lastName;
		$this->gender = $gender;
	}

	public function __toString()//method
	{
		return "Name: $this->firstName $this->lastName Gender: $this->gender";
	}
}

$tom = new Person("Tom", "Grenn", 'm');//creating objects
$elise = new Person("Elise", "Lauda");

echo $tom->firstName;//accessing class property
echo $tom->__toString();//calling a method
```

### Class constants
```php
class Goodbye {
  const LEAVING_MESSAGE = "Thank you for visiting W3Schools.com!";
  public function byebye() {
    echo self::LEAVING_MESSAGE;//have to use self:: here
  }
}

$goodbye = new Goodbye();

$goodbye->byebye();
echo $goodbye::LEAVING_MESSAGE; //calling const variable directly
```
### Static
```php
 <?php
class MyClass {
  public static $str = "Hello World!";//static string

  public static function hello() {//static function
    echo MyClass::$str;
  }
}

echo MyClass::$str;//calling static attribute
echo "<br>";
echo MyClass::hello();//calling static method
?> 
```

### Inheritance
```php
class Person{
	public $firstName;//modifiers = public, private protected
	private $gender;

	public function __construct($firstName,$gender='f'){
		$this->firstName = $firstName;
		$this->gender = $gender;
	}

	public function __toString()//method
	{
		return "Name: $this->firstName Gender: $this->gender";
	}
}

class Employee extends Person{ //employee inherits person
	private $jobTitle;

	public function __construct($firstName, $gender, $jobTitle)
	{
		$this->jobTitle = $jobTitle;
		parent::__construct($firstName, $gender);//calling super(Person) constructor
	}

	public function getJobTitle(){
		return $this->jobTitle;
	}
}

$elise = new Employee("Elise", 'f', "Front-end dev.");
echo $elise;//will call super class to string method
```

### Abstract class
```php
// Parent class
abstract class Car {
    public $name;
    public function __construct($name) {
      $this->name = $name;
    }
    abstract public function intro() : string;
  }
  
// Child classes
class Audi extends Car {
    public function intro() : string {
      return "Choose German quality! I'm an $this->name!";
    }
}
```

### Interface
```php
interface Animal {
  public function makeSound();
}

class Cat implements Animal {
  public function makeSound() {
    echo "Meow";
  }
}

$animal = new Cat();
$animal->makeSound();
```

## CURL
### GET Request
```php
<?php
/* curl didnt work on windows right
go to this website to check curl code: https://paiza.io/projects/3Q8KloXBWiELzAmNf7_xSA */

$curl = curl_init();
$url = "https://jsonplaceholder.typicode.com/posts";

curl_setopt($curl, CURLOPT_URL, $url);//setting curl options
curl_setopt($curl, CURLOPT_RETURNTRANSFER, true);//tell curl to return data rather than just output it.

$resp = curl_exec($curl);// execute the GET request

if($err = curl_error($curl)){
	echo $err;
}else{
	$data = json_decode($resp, true);//return as a array
	// print_r($data); //show all data
	print_r($data[4]["body"]);
}

curl_close($curl);//close the connection
```
### POST Request
```php
<?php
	$curl = curl_init();
	$url = "https://jsonplaceholder.typicode.com/posts";
	
	$data_array = [
		'userId' => 1,
		'id' => 5,
		'title' => "nesciunt quas odio",
		'body' => "repudiandae veniam quaerat sunt sed alias aut fugiat sit"
	];
	
	$data = http_build_query($data_array);//conver array to url encoded format
	
	curl_setopt($curl, CURLOPT_URL, $url);//setting curl options
	curl_setopt($curl, CURLOPT_POST, true);//tell curl to POST
	curl_setopt($curl, CURLOPT_POSTFIELDS, $data);// data to be sent
	curl_setopt($curl, CURLOPT_RETURNTRANSFER, true);
	
	
	$resp = curl_exec($curl);// execute the POST request
	
	if($err = curl_error($curl)){
		echo $err;
	}else{
		$resp = json_decode($resp, true);//json to array
		print_r($resp);
	}
	
	curl_close($curl);//close the connection
```

### PUT Request
```php
<?php
    $curl = curl_init();
    $url = "https://jsonplaceholder.typicode.com/posts/1";

    $data_array = [
        'userId' => 1,
        'id' => 5,
        'title' => "nesciunt quas odio",
        'body' => "repudiandae veniam quaerat sunt sed alias aut fugiat sit"
    ];

    $header = [
        'Authorization: blabla',
        'add more..'
    ];

    $data = http_build_query($data_array);//conver array to url encoded format

    curl_setopt($curl, CURLOPT_URL, $url);//setting curl options
    curl_setopt($curl, CURLOPT_CUSTOMREQUEST, 'PUT');//tell curl ist a PUT request
    curl_setopt($curl, CURLOPT_POSTFIELDS, $data);// data to be sent
    curl_setopt($curl, CURLOPT_RETURNTRANSFER, true);
    curl_setopt($curl, CURLOPT_HTTPHEADER, $header);//send header


    $resp = curl_exec($curl);// execute the POST request

    if($err = curl_error($curl)){
        echo $err;
    }else{
        $resp = json_decode($resp, true);//json to array
        print_r($resp);
    }

    curl_close($curl);//close the connection
```

## File system
### Read file
```php
//read file
$readFile = fopen("newFile.txt", "r") or die("Unable to open file!");
$text =  fread($readFile,filesize("newFile.txt"));

echo $text;
fclose($readFile);
```
### Write file
```php
//write file
$myFile = fopen("newFile.txt", "w") or die("Unable to open file!");//open file or die
$txt = "Jane Doe\n";

fwrite($myFile, $txt);
fclose($myFile);
```
