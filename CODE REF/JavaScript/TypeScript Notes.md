## Data Types
```ts
let name:string = 'john';
let age:number = 34;
let flag:boolean = false;
let array:string[] = ['hello', 'world'];

let role:[number, string] = [32, 'dev']//tuple

//Object
type Person = {
	name:string;
	age?:number;//optional
}

let tommy:Person = {name: 'tommy'};

let people:Person[];

let printName:(name: string)=>number; //input string and output number

//void retuns undefined
//never doesnt return at all

let age:number | string;//age can be a number or string




```