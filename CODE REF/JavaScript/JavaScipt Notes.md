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

## DOM
### Document.write()
```js
document.write(9+3);

document.write('<h1>This is a heading</h1>');
```

## String formatting
```js
let a = 4, b = 5;
let string = "a+b = "+(a+b);

document.write(string);
```
