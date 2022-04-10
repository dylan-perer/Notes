## List 
```tsx
import React, { useEffect, useState } from "react";

const App: React.FC = () => {
  //hooks, give them default values, makes it easier
  const [input, setInput] = useState<string>('');
  const [tasks, setTasks] = useState<Task[]>([]);

  useEffect(() => {
    //add some items to teh list before hand
    let initialTasks: Task[] = [{ taskName: 'initial Task' }, { taskName: 'second task' }]
    setTasks(initialTasks);
  }, []);

  //our own type named Task
  type Task = {
    taskName: string
  }

  //handles getting input from the field
  const onChangeHandler = (e: React.FormEvent<HTMLInputElement>) => {
    setInput(e.currentTarget.value);
    console.log(input);
  }

  //handles adding new Task to the list
  const submitHandler: React.FormEventHandler = (e) => {
    e.preventDefault();
    let newTask: Task = { taskName: input }
    setTasks([...tasks, newTask]);
  }

  //handles removing task
  const handleTaskDelete = (idx:number)=>{
   setTasks(tasks.filter((task:Task, taskNum)=>{
      if(idx!==taskNum){
        return task;
      }
    }));
  } 

  return <div style={style}>
    <h1>Taskify</h1>
    <form onSubmit={submitHandler}>
      <input onChange={onChangeHandler} value={input} placeholder="type something.." type="text" name="input" />
      <button type="submit">Go</button>
    </form>
    {tasks?.map((task: Task, idx: number) => {
      // console.log(task.taskName);
      return <div key={idx}>
        <span>{task.taskName}</span>
        <button type="button" onClick={()=>{handleTaskDelete(idx)}}>Delete</button>
      </div>
    })}
  </div>;
}

const style: React.CSSProperties = {
  margin: '20px'
}

export default App;
```

## Passing JSX Element as a prop
### Parent
```tsx
type UserDetailProp = {
  children: JSX.Element,
  svgStyle: ViewStyle
}

const UserInfo = (props:UserDetailProp) => {
  return (
    ... 
	  {props.children}
	...
  )
}
```
### child
```tsx
const NameScreen = () => {

  return (

    <View>
        <UserInfo svgStyle={styles.svg}><Text></Text></UserInfo>
    </View>
  )
}
```