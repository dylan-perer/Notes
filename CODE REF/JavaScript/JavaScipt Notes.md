# ::: Basics :::
## Where to write JS
```html
<body>
    <!--external -->
    <script src="./index.js"></script>
    
    <!--internal-->
    <script>
        //code
    </script>
</body>
```

## Variables
```js
let myName = "Dyaln"; //let is scope bound
var iLike = "pizza"; //can be re  declared, wtf lol
const PI = 3.141// final, cannot be reassigned
```

### Data Types
```js
//Primitives 
let x = 18; //is a number, can be any number so floats
let y = "dylan";//is a string
let flag = true;//is bool

let p;//p is undefined

let num = null;//null is a object, so num = object

document.write(typeof(x)+"\n")
document.write(typeof(y)+"\n")
document.write(typeof(flag)+"\n")
document.write(typeof(p)+"\n")
document.write(typeof(num)+"\n")

```

### Type Conversion
```js
let num = 43;
console.log(typeof(String(num)));//converting number to a string

let str = "43"; //also can use parseInt(str) or parseFloat(str)
console.log(typeof(Number(str)));//converting string to a number

let flag = false;
console.log(typeof(String(false)));//converting bool to a string

let flag2 = true;
console.log(typeof(Number(flag2)));//converting bool to a number, prints 1
```

## Conditionals
### If else
```js
if(4%2===0){ // if, else if, else
    console.log("Even number");
}else{
    console.log("Odd number");
}
```

### Switch
```js
let day = 3;

switch (day) {
  case 1:
    console.log("Sunday");
    break;
  case 2:
    console.log("Monday");
    break;
  case 3:
    console.log("Tuesday");
    break;
  case 4:
    console.log("Wednesday");
    break;
  case 4:
    console.log("Thursday");
    break;
  case 5:
    console.log("Friday");
    break;
  case 6:
    console.log("Saturday");
    break;
  default:
    console.log("Don't know bruh!");
}
```

## Loops
### For loop
```js
let str = "this is a string";

for(let i = 0; i<str.length;i++){
    document.write(str[i]);
    document.write('<br>');
}
```

### While
```js
let count = 0;
while(count<=5){
    document.write(count);
    document.write('<br>');
    count++;
}
```
#### Do While
```js
let count=0;
do{
    document.write(count);
    document.write('<br>');
    count++;
}while(count<=5);
```

## Functions
```js
function add(x, y){
    return x+y;
}

document.write(add(5,4));

```
## Strings 
### Methods
```js
let str = "some text in \"quotes\".";//escaping
let strLength = str.length;//length
str.toUpperCase();//uppercase & lowercase

console.log(str.includes("text"))//find sub string in string, returns boolean
console.log(str.startsWith("some"))//check string initial with the substring, return boolean | endsWith()
console.log(str.replace("text", "texts"))//replace
console.log(str.indexOf("in"))//returns the start index of in
console.log(str.split(" "))//split by spaces, returns array
console.log(str.slice(3,15))//returns substring, startIndex, endIndex
```
### Formating 
```js
str = `here is text ${1+2} more text`;
console.log(str);
```

## Arrays
```js
let array = ["a pig", "a dog", "a rat", 2, ["second array", 3], "pop me"];
array.pop();// pop the last element
array.push("a bird");//insert new element

for(let i=0;i<array.length;i++){
    console.log(array[i]);
}
```
### Array Map
```js
//manipulate each element in array and return new array
let array = [1,2,3,4,5];

array = array.map((element, idx)=>{
    return element*2; //times each element in the array by 2
	//idx = index
});
```

### Filter
```js
//removing item from a array
people = people.filter((person)=>{
      if(person.id !== id){
        return person;
      }
});
```
### Reduce
```js
let array = [1,2,3,4,5];

array = array.reduce((accumulator, currentValue)=>{//sum of all the elements
    return accumulator + currentValue
})

console.log(array);
```

### Key pair
```js
var myArray = {id1: 100, id2: 200, "tag with spaces": 300};
myArray.id3 = 400;
myArray["id4"] = 500;

for (var key in myArray) {
  console.log("key " + key + " has value " + myArray[key]);
}
```
## Objects
### Method: 1
```js
vehicle = {
    make: "Yamaha",
    model: "R6",
    engine: "600cc",
    weight: 190,

    //method inside a object
    type: function(){
        return "Motorcycle";
    }
}

console.log(vehicle);
console.log(vehicle.type());

```

### Method: 2
```js
function vehicle(make, model, price){
    this.make = make;
    this.model = model;
    this.price = price;

    this.getPrice = function(){
        return price;
    }
}

let audi = new vehicle("Audi", "Q7", "67000NZD")
console.log(audi);
console.log(audi.getPrice());
```
## Math
```js
console.log(Math.PI);
console.log(Math.E);
console.log(Math.floor(4.32));
console.log(Math.sqrt(5));
console.log(Math.max(5, 10));
console.log(Math.abs(-29));
console.log(Math.pow(2,6));
```
## Date
```js
let now = new Date();
console.log(new Date());

console.log(new Date(2018, 11, 24)); //y-month(starts from 0)-day
console.log(now.getDay());
```
## Timer
### Delayed execution
```js
function doSomething() {
    console.log("bird");
}

setTimeout(doSomething, 3000);
```
### Repeated execution
```js
let i=0;
let id = setInterval(() => {// similar to java sleep
  document.getElementById("myH1").innerHTML = i++;
  if(i===30){
      clearInterval(id);
  }
}, 100);

```

## Random number
```js
function getRndInteger(min, max) {
  return Math.floor(Math.random() * (max - min + 1) ) + min;
}
```

## Spreading
```js
const Book = ({title, img, author}) => {//spread object, nested spreading = ({variable ,obj{}})
	//code
}
```
## Import & Export (ES6)
```js
//:: data.js ::
export const data = [
    {
        img: "https://images-na.ssl-images-amazon.com/images/I/51PRQuO-xjL._SX218_BO1,204,203,200_QL40_FMwebp_.jpg",
        author: "Ann Whitford",
        title: "If Animals Kissed Good Night",
    },
    {
        img: "https://images-na.ssl-images-amazon.com/images/I/51VQB3uWu+L._SX258_BO1,204,203,200_.jpg",
        author: "Alice Schertle",
        title: "Little Blue Truck's Springtime",
    },
    {
        img: "https://images-na.ssl-images-amazon.com/images/I/512kHsHZHNL._SY497_BO1,204,203,200_.jpg",
        author: "Sandra Boynton",
        title: "The Going-To-Bed Book",
    },
]

export const data2 = [
    {
        img: "https://images-na.ssl-images-amazon.com/images/I/51PRQuO-xjL._SX218_BO1,204,203,200_QL40_FMwebp_.jpg",
        author: "Ann Whitford",
        title: "If Animals Kissed Good Night",
    }
]

// importing in a different file
import {data,data2} from './data';//named exporting | name must be the same
```

## DOM
### Document.write()
```js
document.write(9+3);

document.write('<h1>This is a heading</h1>');
```

### Get elements
```js
 //get by id and change text
document.getElementById("myH1").innerHTML = "My name is Dylan.";

//get by class and change text, returns a array
document.getElementsByClassName("myDivs")[1].innerHTML = "0";

//get by tag name, returns a array
document.getElementsByTagName("div")[2].innerHTML = "99";
```
### Event handlers
```js
const myH1 = document.getElementById("myH1");

myH1.onclick = function(){
    document.write("Clicked!!");
}
```

## Try catch
```js
let i = 100;
let j = 0;

try {
    if(j==0){
        throw "j cannot be zero";
    }
} catch (error) {
    console.log(error);
}

try {
    let k = 9000/0; // lol it returns infinity!
    console.log(k);
} catch (error) {
    console.log(error);
}finally{
    console.log("done");
}
```
# ::: Advanced :::
## ECMAScript
```js
//ECMAScript is another name for JavaScript
//ES 6 is the most features introduced
```

## V8 engine
```js
//converts js to machine code
```
## NodeJs
```js
// js on servers
//NodeJS gave js file access, networking, and utils to write server-side js code
```

## JIT
```js
//doesn't need to be compiled like java or c++
//turns js to machine code on the fly when it needs to be
```

## Call Stack
![[Screenshot 2022-02-28 212651.png]]

### Task Queue
```js
/*When u have async code -
	1. it is pushed to the task queue, not the call stack
	2. when the call stack is empty and the async code is done then it will be pushed into the call stack
```

###  Microtasks Queue
```js
/*microtask queue is emptied/exhausted before task queue
	1. promises are placed on the microtask queue

```

## Fetch API
### Callbacks
```json
//callbacks are old way of doing it, Promises are the new way
function firstFunction(arg1, callback){
    //do stuff
    callback();//call the callback function
}
```

### Promises
```js
/* 
    Promises are async code
    it has 3 States:
        1. pending
        2. fulfilled
        3. rejected
*/

const myPromise = new Promise((resolve, reject)=>{
    const error = false;
    if(!error){
        resolve("Yes! resolved the promise");
    }else{
        reject("No! rejected the promise");
    }
});

myPromise.then((value)=>{//getting the value out of the promise
    console.log(value);
}).catch(err =>{
    console.log(err);// if error true
})
```

#### Calling fetch with promise
```js
//fetch is a promise
users = fetch("http://jsonplaceholder.typicode.com/users")
    .then((res)=>{
        console.log(res);//res = readableStream
        return res.json();//data is not ready to be read yet, turn stream into json | json() is a promise
    }).then((res)=>{
        console.log(res);//data is ready
    })

console.log(users);//we can't get the data because fetch is still pending | DONT DO THIS!!
```

### Async / await
```js
//Async / await, syntactic sugar for promises, looks way cleaner
const myCoolFunc = async () =>{
    const response = await fetch("http://jsonplaceholder.typicode.com/posts");
	if(response.status===200){
	    const jsonPostData = await response.json();
	    return jsonPostData; //data is ready
	}
}

const mySecondCoolFunc = async ()=>{//chaining
    const data = await myCoolFunc();
    console.log(data);
}

mySecondCoolFunc();
```

### GET
```js
const getDadJoke = async ()=>{
    let res = await fetch("https://icanhazdadjoke.com/",{
        method: "GET",
        headers: {
            Accept: "application/json" //type of data to accept
        }
    });
    res = await res.json();
    console.log(res.joke);
}

getDadJoke();
```

### POST
```js
const joke = {
  id: "dprjbhyAAAd",
  joke: "A Sandwich walks into a bar, the bartender says “Sorry, we don’t serve food here”",
};

const postDadJoke = async (jokeObj) => {
  let res = await fetch("https://httpbin.org/post", {
    method: "POST",
    headers: {
      "Content-Type": "application/json", //type of data to send
    },
    body: JSON.stringify(joke)
  });
  res = await res.json();
  console.log(res.headers);
};

postDadJoke(joke);
```