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
npx create-react-app ts-demo --template typescript; # typescript
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

### Prop Types (validating props)
```jsx
import React from 'react';
import PropTypes from 'prop-types';//1. import prop types module
import defaultImage from '../../../assets/default-image.jpeg';

const Product = ({ image, name, price }) => {
  const url = image && image.url;//if image object and image.url exists
  return (
    <article className='product'>
      <img src={url || defaultImage} alt={name || 'default name'} />
      <h4>{name}</h4>
      <p>${price || 3.99}</p>{/**show price if exists, if not show default */}
    </article>
  );
};

//2. setting what props are required | now program wont break but returns warnings if something required is missing
Product.propTypes = {
  image: PropTypes.object.isRequired,
  name: PropTypes.string.isRequired,
  price: PropTypes.number.isRequired,
};
//3. defaults, if we want to setup up incase prop required fails
Product.defaultProps = {
  name: 'default name',
  price: 3.99,
  image: defaultImage,
};

export default Product;
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
#### Why use UseRef
```jsx
import React, { useEffect, useRef } from 'react';
// similar to useState
// DOES NOT trigger re-render
// target DOM nodes/elements
const UseRefBasics = () => {
  const refContainer = useRef(null);

  //set focus on input field
  useEffect(() => {
    console.log(refContainer.current);//this is return the DOM element i.e. <h1>text</h1>
    refContainer.current.focus();//we can just call it inside useEffect, useRef doesn't rerender 
  });

  return (
    <>
      <form className='form' onSubmit={handleSubmit}>
        <div>
          {/**ref can be used on any html element */}
          <input type='text' ref={refContainer} />
        </div>
        <button type='submit'>submit</button>
      </form>
    </>
  );
};

export default UseRefBasics;

```

### Use Reducer
#### Why use UseReducer
```jsx
//use reducer is very similar to useState()
//it will cause a rerender

import { useReducer } from "react";
import ReactDOM from "react-dom";

const initialTodos = [
  {
    id: 1,
    title: "Todo 1",
    complete: false,
  },
  {
    id: 2,
    title: "Todo 2",
    complete: false,
  },
];

const reducer = (state, action) => {//reducer handler
  switch (action.type) {
    case "COMPLETE"://action name
      return state.map((todo) => {
        if (todo.id === action.id) {
          return { ...todo, complete: !todo.complete };
        } else {
          return todo;
        }
      });
    default:
      return state;
  }
};

function Todos() {
  const [todos, dispatch] = useReducer(reducer, initialTodos);

  const handleComplete = (todo) => {
    dispatch({ type: "COMPLETE", id: todo.id });//calling dispatch on reducer
  };

  return (
    <>
      {todos.map((todo) => (
        <div key={todo.id}>
          <label>
            <input
              type="checkbox"
              checked={todo.complete}
              onChange={() => handleComplete(todo)}
            />
            {todo.title}
          </label>
        </div>
      ))}
    </>
  );
}

ReactDOM.render(<Todos />, document.getElementById('root'));
```

### Use Context
#### Why use UseContext
```jsx
/*
	TO PASS DATA
	removes drop drilling (passing DATA all the way from TOP component to the BOTTOM)
*/
import React, { useState, useContext } from 'react';
import { data } from '../../../data';
// more components
// fix - context api, redux (for more complex cases)

const PersonContext = React.createContext();
// two components - Provider, Consumer

const ContextAPI = () => {
  const [people, setPeople] = useState(data);
  const removePerson = (id) => {
    setPeople((people) => {
      return people.filter((person) => person.id !== id);
    });
  };
  return (
    //wrap the root component with context we created and pass the values
    <PersonContext.Provider value={{ removePerson, people }}>
      <h3>Context API / useContext</h3>
      <List />
    </PersonContext.Provider>
  );
};

const List = () => {
  const mainData = useContext(PersonContext);
  console.log(mainData);
  return (
    <>
      {mainData.people.map((person) => {
        return <SinglePerson key={person.id} {...person} />;
      })}
    </>
  );
};

const SinglePerson = ({ id, name }) => {
  const { removePerson } = useContext(PersonContext); //here we have the data from the context

  return (
    <div className='item'>
      <h4>{name}</h4>
      <button onClick={() => removePerson(id)}>remove</button>
    </div>
  );
};

export default ContextAPI;

```

### Custom hooks
#### Why use custom hooks
```jsx
//to create custom functionality to your website
//heere is a custom fetch hook
import { useState, useEffect, useCallback } from 'react';

//make sure to name it use[Name]
export const useFetch = (url) => {
  const [loading, setLoading] = useState(true);
  const [products, setProducts] = useState([]);

  const getProducts = useCallback(async () => {
    //fetch the data
    const response = await fetch(url);
    const products = await response.json();
    setProducts(products);

    setLoading(false);
  }, [url]);

  useEffect(() => {
    getProducts();
  }, [url, getProducts]);//every time we pass a new url useEffect will run

  //return the states
  return { loading, products };
};


//using the hook outside
const { loading, products } = useFetch(url)
console.log(products)

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

## Router
### Installing react-router
```shell
npm i react-router-dom
```

```jsx
import React from "react";
//import react router
import {
  BrowserRouter as Router,
  Route,
  Switch,
} from "react-router-dom/cjs/react-router-dom.min";
//pages
import Home from "./tutorial/11-react-router/setup/Home";
import About from "./tutorial/11-react-router/setup/About";
import Error from "./tutorial/11-react-router/setup/Error";
import Navbar from "./tutorial/11-react-router/setup/Navbar";

function App() {
  return (
    <Router>
      <Navbar/>
      <Switch>{/**only the first one that matches gets displayed */}
        <Route exact path={"/"}>{/**add exact so it does match with other paths / */}
          <Home />
        </Route>
        <Route exact path={"/about"}>
          <About />
        </Route>
        <Route path="*">
          <Error />
        </Route>
      </Switch>
    </Router>
  );
}

export default App;

```

```jsx
//Nav
import React from "react";
import { Link } from "react-router-dom";
//make sure to use react-router <Link/> components for <a> tags
const Navbar = () => {
  return (
    <nav>
      <ul>
        <li>
          <Link to="/">Home</Link>
        </li>
        <li>
          <Link to="/about">About</Link>
        </li>
      </ul>
    </nav>
  );
};

export default Navbar;
```
### Dynamic URLs (lists)
```jsx
//  1. add routes to the Router
<Route exact path={"/people"}><People/></Route>{/**people is a list */}
<Route exact path="/person/:id" children={<Person/>}>{/**person will be the item with a dynamic url */}

{/* 2.  inside the array add a link element to the items*/}
{people.map((person) => {
return (
  <div key={person.id} className='item'>
	<h4>{person.name}</h4>
	<Link to={`./person/${person.id}`}>See more info</Link>
  </div>
);

{/* 3. accessing url parameter from the item*/}
import { Link, useParams } from 'react-router-dom';
const Person = () => {
  const { id } = useParams();//get this from url passed down from list
  return (
    <div>
      <h2>{id}</h2>
      <h2>person</h2>
    </div>
  );
};
```
## Optimization
```jsx
// use memo's and callback to optimize
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