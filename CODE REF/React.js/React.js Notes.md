## What is React.js?

```js
//React is a javascript library to create user interfaces.
```
### It's all about components
```js
//you can think of a component as a small chunk of UI | lego blocks | reusability 
```
### Virtual DOM
```js
//React uses virtual DOM so only the effect elements will be updated rather than the whole DOM
```

## Getting started
```js
/* 
	1. install node
	2. install react dev tools addon on the browser
	3. New dir 
*
```

```shell
npx create-react-app app-name;
npm start
```

### Entry
```js
/*
	1. public/index.html is the entry for the website
	2. inside inde.html > div with id root is where all our code will live
*
```

### Build
```shell
npm run build
```

## Component
### Create & render a component
```jsx
import React from 'react';
import ReactDom from 'react-dom';

//make sure to Capitalize 1st letter of the function name so react can see.
const Greeting=()=>{//this is a component
  return <h4>Welcome to the app!</h4>;//return jsx
}

//render the component into ROOT
ReactDom.render(<Greeting/>, document.getElementById('root'));
```

### Fragment
```jsx
const Greeting = () => {
  return (
    <>{/*this is a fragment, component can only return on element, so if u have more you can wrap around a fragment*/}
      <div>
        <h2>Heading</h2>
      </div>
      <div><h3>Heading 3</h3></div>
    </>
  );
};
```

### Nested components
```jsx
const Greeting = () => {
  return (
    <div>
      <h2>Hello!</h2>
      <Person />
    </div>
  );
};

const Person = () => {
  return <h4>Jane Doe</h4>;
};
```

### JSX CSS
```jsx
import React from "react";
import ReactDom from "react-dom";
import "./index.css"; //import external css | good idea to have set default styles there

const imgeUrl =
  "https://images-na.ssl-images-amazon.com/images/I/51p2SDOCV9L._SX218_BO1,204,203,200_QL40_FMwebp_.jpg";
const BookList = () => {
  return (
    <section>
      <Book />
      <Book />
    </section>
  );
};

const Book = () => {
  return (
    <article style={styles.book.container}>
      <img src={imgeUrl} style={{padding: '0px'}} alt="" />
      {/* using {} we can inject js code to jsx */}
      <h4>I Love you to the Moon and Back</h4>
      {/*calling css object, these css will become inline, so it will override the external css*/}
      <p style={styles.book.authorName}>Amelia Hepworth</p>
    </article>
  );
};

//css styles object
const styles = {
  book: {
    container:{
      display: 'grid',
      background: 'white', 
      margin: 'auto', 
      maxWidth: '400px', 
      justifyContent: "center", 
      borderRadius: '20px',
      padding: '15px',
      marginBottom: '10px'
    },
    image:{
      
    },
    authorName: {
      color: "#617d98",
      fontSize: "16px",
    },

  },
};

ReactDom.render(<BookList />, document.getElementById("root"));

```

### Exporting and Importing
```js
// we can use the ES6 module to export and import, so

export default Book;//exporting book component from Book.js file
import Book from './Book'; // we can name book anything because it default export
```

## Utils
### Sample images
https://picsum.photos/
```jsx
const imgUrl = 'https://picsum.photos/seed/picsum/200/300'
```
## Props
```jsx
const BookList = () => {
  return (
    <section>
      {/*passing props to the component Book*/}
      <Book title='title' author='some author' img='https://picsum.photos/seed/picsum/200/300'/>
      <Book title='title2' author='some author2' img='https://picsum.photos/seed/picsum/200/300'/>
    </section>
  );
};

const Book = ({title, img, author}) => {//spread object, nested spreading = ({variable ,obj{}})
  return (
    <article style={styles.book.container}>
      <img src={img} style={{padding: '0px'}} alt="" />
      <h4>{title}</h4>
      <p style={styles.book.authorName}>{author}</p>
    </article>
  );
};
```
### Children prop
```jsx
const BookList = () => {
  return (
    <section>
      <Book title='title' author='some author' img='https://picsum.photos/seed/picsum/200/300'>
        {/* this is a child prop of Book */}
        <p>Nisi mollit est nostrud pariatur consequat eu fugiat cupidatat.</p>
      </Book>
    </section>
  );
};

const Book = ({title, img, author, children}) => {//children is a property of prop object
  return (
    <article style={styles.book.container}>
      <img src={img} style={{padding: '0px'}} alt="" />
      <h4>{title}</h4>
      <p style={styles.book.authorName}>{author}</p>
      {children}{/*access the children prop */}
    </article>
  );
};
```
## Displaying a list
```jsx
const booksData = [/*objetcs...*/];

const BookList = () => {
  return (
    <section>
      {bookData.map((book,idx)=>{//mapping array 
        //passing array element(object) properties as props to Book component
        return <Book key={idx} {...book}/>//spread book, i.e. title={book.title} author={book.author}
      })}
    </section>
  );
};

const Book = ({img, author, title}) => {
  return //jsx
};
```
## Event listener
```jsx
const Book = ({img, author, title}) => {
  const clickHandler = () =>{//event handler function | u can always have this as a inline anonymous
    alert('hello world')
  }
  return (
    <article style={styles.book.container}>
      <p style={styles.book.authorName}>{author}</p>
      {/*on click event listener */}
      <button onClick={clickHandler}>click here</button>
    </article>
  );
};
```
### Passing arguments
```jsx
const Book = ({img, author, title}) => {
  const clickHandler = (author) =>{//event handler function | u can always have this as a inline anonymous
    alert(`author is ${author}`);
  }
  return (
    <article style={styles.book.container}>
      <p style={styles.book.authorName}>{author}</p>
      {/*passing params will require to wrap the handler in a anonymous function */}
      <button style={styles.book.button} onClick={()=>{clickHandler(author)}}>See more info</button>
    </article>
  );
};
  
```
# ::: Advanced :::
```jsx
//code
```
## Hooks
### Why use hooks?
```jsx
//To make our page dynamic and stateful
```
### Use State
```jsx
import React, { useState } from "react";

//useState will trigger a render of the element 
const UseStateBasics = () => {
  //text is a variable, setText is a function
   const [text, setText] = useState("default title");

  const onClickHandler =()=>{
    text==="default title"?  setText('random title'): setText('default title');
  }
  return (
    <>
      <h2>{text}</h2>
      <button type="button" className="btn" onClick={onClickHandler}>Change title</button>
    </>
  );
};

export default UseStateBasics;

```
#### Funtional way
```js
const [text, setText] = useState("default title");
setText((prevValue)=>{return prevValue})//use this if you want the exact previous value
```
#### Array example
```jsx
// removes a single item form the array using a index
import React from "react";
import { useState } from "react";
import { data } from "../../../data";

const UseStateArray = () => {
  let [people, setPeople] = useState(data);

  const removePersonHandler = (id) => {
    people = people.filter((person)=>{
      if(person.id !== id){
        return person;
      }
    });
    setPeople(people);
  };

  return (
    <>
      <h2>useState array example</h2>
      {people.map((person) => {
        return (
          <>
            <Person key={person.id} removePersonHandler={removePersonHandler} {...person}
            />
          </>
        );
      })}
    </>
  );
};

const Person = ({ id, name, removePersonHandler }) => {
  return (
    <div className="item">
      <p>
        <span>{id}: </span>
        {name}
      </p>
      <button className="btn" onClick={() => {removePersonHandler(id);}}>
        remove
      </button>
    </div>
  );
};

export default UseStateArray;

```
#### Object example
```jsx
const [person, setPerson] = useState({name: 'boby', message: 'hello world'});

//now when calling setPerson
setPerson({...person, message: 'hello nz'})//use spread operator to copy the existing values, then pass the values we want to edit
```
### Use Effect
#### Why use UseEffect
```jsx
// Use useEffect when you have to do some work outside the component
// useEffect will run after every re-render


function App() {
  const [title, setTitle] = useState('you have no messages');
  const [messages, setMessages] = useState(0);
  
  useEffect(()=>{
    //run on every rerender
    //2nd argument, run only on these variable changes | empty[] will mean only run once at the start
    if(messages>=1){
      setTitle(`You have ${messages} messages!`);
    }
  },[messages])
  return (
    <div className='container'>
      <h3>{title}</h3>
      <button onClick={()=>{setMessages(messages+1)}} className="btn">add new messages</button>
    </div>
  )
}
```
#### Cleanup
```jsx
  useEffect(()=>{
    if(messages>=1){
      setTitle(`You have ${messages} messages!`);
    }
    console.log("useEffect called");
    return () =>{//triggers after use effect | use this to cleanup. i.e. removing a eventListener | avoid memoryleaks
      console.log('cleanup');
    }
  },[messages])
```
#### Fetch data
```jsx
  const [users, setUsers] = useState([]);

  let fetchUsers = async () => {
	  let res = await fetch(url);
	  if(res.status===200){
		res = await res.json();
		setUsers(res);
	  }
  };

  useEffect(() => { //execute on component render once
    fetchUsers();
  }, []);
```

### Use Ref
#### Why use
```jsx
//code
```

#### title
```jsx
//code
```

#### title
```jsx
//code
```

## Forms
```jsx
import React, {useState} from "react";

function App() {
  const [fName, setFname] = useState('');
  const [email, setEmail] = useState('');
  const handleSubmit = (e)=>{
    e.preventDefault();//stop the default form submission (reload)
    console.log(`${fName} ${email}`);
    //do something with the input
  }
  return (
    <>
      <form className="form" onSubmit={handleSubmit}>
        <label htmlFor="fName">Name: </label>
        {/**first we bind input field to a state variable 
         * then using onChange's=> event.target.value we set state
        */}
        <input value={fName} onChange={(e)=>{setFname(e.target.value)}} type="text" id="fName" name="fName" placeholder="name"/>
        <br></br><br></br>
        <label htmlFor="email">e-mail: </label>
        <input value={email} onChange={(e)=>{setEmail(e.target.value)}} type="text" id="email" name="email" placeholder="email"/>
        <button type="submit" className="btn">Add Person</button>
      </form>
    </>
  );
}

export default App;
```
### Large form
```jsx
import React, { useState } from 'react';

const ControlledInputs = () => {
  //use a object for the inputs
  const [person, setPerson] = useState({ firstName: '', email: '', age: '' });
  const [people, setPeople] = useState([]);
  
  //one function to handle all properties in the object
  const handleChange = (e) => {
    const name = e.target.name;//this will return the input field name, i.e. firstName
    const value = e.target.value;//this will return the input field value, i.e. john
    
    //(we dont want to delete other fields while we update one)
    //spread all the person's obj properties, then modify the new values
    //firstName: john
    setPerson({ ...person, [name]: value });
  };


  const handleSubmit = (e) => {
    e.preventDefault();//prevent on submit reload
    if (person.firstName && person.email && person.age) {//checks if any inputs are empty
      //handles adding the new person into a list and set state variable
      const newPerson = { ...person, id: new Date().getTime().toString() };
      setPeople([...people, newPerson]);
      setPerson({ firstName: '', email: '', age: '' });
    }
  };
  return (
    <>
      <article className='form'>
        <form>
          <div className='form-control'>
            <label htmlFor='firstName'>Name : </label>
            <input
              type='text'
              id='firstName'
              name='firstName'
              value={person.firstName}
              onChange={handleChange}
            />
          </div>
          <div className='form-control'>
            <label htmlFor='email'>Email : </label>
            <input
              type='email'
              id='email'
              name='email'
              value={person.email}
              onChange={handleChange}
            />
          </div>
          <div className='form-control'>
            <label htmlFor='age'>Age : </label>
            <input
              type='number'
              id='age'
              name='age'
              value={person.age}
              onChange={handleChange}
            />
          </div>
          <button type='submit' className='btn' onClick={handleSubmit}>
            add person
          </button>
        </form>
      </article>
      <article>
        {people.map((person) => {
          const { id, firstName, email, age } = person;
          return (
            <div key={id} className='item'>
              <h4>{firstName}</h4>
              <p>{email}</p>
              <p>{age}</p>
            </div>
          );
        })}
      </article>
    </>
  );
};

export default ControlledInputs;

```

## Title
```jsx

```

## Title
```jsx

```

## Title
```jsx

```

## Title
```jsx

```

## Title
```jsx

```

## Unit Testing:: TODO