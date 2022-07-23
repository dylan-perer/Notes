## What is redux
### 3 core concepts
![[Screenshot 2022-07-23 105730.png]]

## The Three Principles
##### First principle
<i>The sate of you whole application is stored in an object tree within a single store</i>

##### Second principle
<i>The only way to chnage the state is to emit and action, an object decibing what happned</i>

##### Third principle
<i>To descibe how the state tree should change by a action, we write reducers</i>
```js
//reducer - (prevState, action) =>newState
```

### Pros & cons
```jsx
//Redux is a state management library for js apps
//Synchronizes data across all UIs
//functional programming

/*
	pros: {
		predictable state changes
		centralized stae
		easy debuging
	}

	cons:{
		complexity
		boilerplates
	}
*
```
## Installing redux
```shell
npm i redux react-redux
```

## Essence of redux
### Action
```js
import redux from 'redux'

//store has 3 functions
//getState() - returns current state
//dispacth(action) - allows us to update state with a new action
//subscribe(listener) - allows us to register listners
const createStore = redux.createStore;
const combineReducers = redux.combineReducers

//inital states
const initialCakeState = {
	numOfCakes: 10
}

const initialIceCreamState = {
	numOfIceCream: 20
}

//simple action
const BUY_CAKE = 'BUY_CAKE'
const BUY_ICE_CREAM = 'BUY_ICE_CREAM'

function buyCake(){
	return {
		type: BUY_CAKE
		info: 'Bought a cake'
	}
}

function buyIceCream(){
	return {
		type: BUY_ICE_CREAM
		info: 'Bought a icecream'
	}
}
```

### Reducer
```js

//reducer
// (prevState, action) => newState
const cakeReducer = (state = initialCakeState, action) => {
	switch(action.type){
		case BUY_CAKE: return {
			...state
			numOfCakes: state.numOfCakes - 1
		}
		default: return state
	}
}

const iceCreamReducer = (state = initialIceCreamState, action) => {
	switch(action.type){
		case BUY_ICE_CREAM: return {
			...state
			numOfCakes: state.numOfIceCream - 1
		}
		default: return state
	}
}


//define the root reducer
const rootReducer = combineReducers({
	cake: cakeReducer,
	iceCream: iceCreamReducer
});

```

### Store
```js

//creating the store
const store = createStore(rootReducer);
console.log('Initial state', store.getState());

//add a listener
const unsubscribe = store.subscribe(()=>console.log('Updated state',store.getState()));

//execute actions
store.dispatch(buyCake());
store.dispatch(buyIceCream());

unsubscribe();//removing listener
```

## Async Actions
```js
import redux from 'redux'

const createStore = redux.createStore;

const initialState = {
	loading: false,
	users: [],
	error: ''
}

//actions
const FETCH_USERS_REQUEST = 'FETCH_USERS_REQUEST'; 
const FETCH_USERS_SUCCESS = 'FETCH_USERS_SUCCESS'; 
const FETCH_USERS_FAILURE = 'FETCH_USERS_FAILIURE';

const fetchUsersRequest = () => {
	return {
		type: FETCH_USERS_REQUEST,
	}
}

const fetchUsersSuccess = (users) => {
	return {
		type: FETCH_USERS_SUCCESS,
		payload: users
	}
}

const fetchUsersFailure = (error) => {
	return {
		type: FETCH_USERS_FAILURE,
		payload: error
	}
}

//reducer
const userReducer = (state = initialState, action) => {
	switch(action.type){
		case FETCH_USERS_REQUEST:
		return {
			...state,
			loading: true
		}
		
		case FETCH_USERS_SUCCESS:
		return {
			...state,
			loading: false,
			users: action.payload,
			error: ''
		}
		
		
		case FETCH_USERS_FAILURE:
		return {
			...state,
			loading: false,
			users: [],
			error: action.error
		}
	}
}

//action creator, this will return a action
const fetchUsers = () => {
	return function(dispatch) {
		dispatch(fetchUsersRequest())
		axions.get('url')
			.then(response => {
				dispatch(fetchUsersSuccess(response.data))
			})
			.catch(error => {
				dispatch(fetchUsersFailure(response.error))
			})
	}
}

//store
createStore(userReducer, applyMiddleware(thunkMiddleWare));
const unsubscribe = store.subscribe(()=>console.log('Updated state',store.getState()));

store.dispatch(fetchUsers())
```

## Redux and React

### Action 
./src/redux/cake/cakeTypes.js
```jsx
//<cakeTpes.js>
export const BUY_CAKE = 'BUY_CAKE'
```
./src/redux/cake/cakeAction.js
```js
//<cakeActions.js>
import {BUY_CAKE} from ',/cakeTypes'

function buyCake(number = 1){
	return {
		type: BUY_CAKE,
		payload: number,
		info: 'Bought a cake'
	}
}
```
### Reducer
./src/redux/cake/cakeReducer.js
```js
//<cakeReducer.js>
import {BUY_CAKE} from ',/cakeTypes'

const initialCakeState = {
	numOfCakes: 10
}

const cakeReducer = (state = initialCakeState, action) => {
	switch(action.type){
		case BUY_CAKE: return {
			...state
			numOfCakes: state.numOfCakes - action.payload
		}
		default: return state
	}
}

export default cakeReducer;

```

### Store
./src/redux/store.js
```js
//<store.js>
import {createStore, applyMiddleware} from 'redux'
import logger from 'redux-logger'
import cakeReducer from './cake/cakeReducer'

const store = createStore(cakeReducer, applyMiddleware(logger))
export default store

//<App.js>
import store from './redux/store'
import {Provider} from 'react-redux'

...

	function App(){
		return (
			<Provider store={store}>
				<div className='App'>
					<CakeContainer/>
				</div>
			</Provider>
		)
	}
...
```

### Maping props to component
Dispatch a action from component

./src/redux/index.js
```js
//<index.js>
export {buyCake } from './cake/cakeActions'
```

```jsx
import {connect} from 'react-redux'

import {buyCake} from './redux'

const CakeContainer = (props) => {
	const [number, setNumber]  = useState(1);
	
	return (
		<div>
			<h2>Number of cakes - {props.numOfCakes}</h2>
			<input type='text' value={number} onChange={e => setNumber(e.target.value)}/>
			<button onClick={() => props.buyCake(number)}>Buy Cake</button> {/*dispatch action from this button*/}
		</div>
	)
}

//map redux state to props
const mapStateToProps = (state) => {
	return {
		numOfCakes: state.numOfCakes //now CakeContainer will receive a aditional prop -> numOFCakes
	}
}


const mapDispatchToProps = dispatch => { //a action we can now use in our component 
	return {
		buyCake: (number) => dispatch(buyCake(number))
	}
}
export default connect(mapStateToProps, mapDispatchToProps)(CakeContainer)//connects the component to redux store
```

## Redux dev tools
![[Screenshot 2022-07-23 132532.png]]

## Redux hooks
