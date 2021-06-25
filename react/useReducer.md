# useReducer
haddle..관련 함수코드는 줄이고 간단하게 표현 할 수 있습니다. 
```
import React, {useState, useReducer} from 'react'

const ACTIONS = {
  INCREMENT : 'increment',
  DECREMENT : 'decrement'
  }
  
function reducer(state, action){
  switch (action.type){
    case ACTIONS.INCREMENT:
      return { count : state.count + 1 }
     case ACTIONS.DECREMENT :
      return { count : state.count - 1 }
     default:
      return state
    }
  }
  
export default function App(){
  const [state, dispatch] = useReducer(reducer, {count : 0})
  
  function increment(){
    dispatch({type : ACTIONS.INCREMENT })
   }
   
   function decrement(){
    dispatch({type : ACTIONS.DECREMENT })
   }
   
   return(
   <>
    <button onClick={decrement}> - </button>
    <span>{state.count}</span>
    <button onClick={increment}> + </button>
   </>
   )
 }
```

```
import React, {useState, useReducer} from 'react'

const ACTIONS = {
  ADD_TODO : 'add-todo',
  TOGGLE_TODO : 'toggle-todo',
  DELETE_TODO : 'delete-todo'
 }
  
function reducer(todos, action){
  switch (action.type){
    case ACTIONS.ADD_TODO:
      return [...todos, newTodo(action.payload.name)]
     case ACTIONS.TOGGLE_TODO:
      return todos.map(todo => {
        return todo.id === action.payload.id ? {...todo, complete: !todo.complete} : todo
      })
      case ACTION.DELETE_TODO:
       return todos.filter(todo => todo.id !== action.payload.id)
      default:
        return todos
     }
     case ACTION.DELETE_TODO:
      return todos.filter(todo => todo.id !== action.payload.id)
   }

   
function newTodo(name){
  return { id : Date.now(), name: namem, complete: false }
}

export default function App(){
  const [todos, dispatch] = useReducer(reducer, [])
  const [name, setName] = useState('')
  
function handleSubmit(e){
  e.preventDefault()
  dispatch({type:ACTIONS.ADD_TODO , payload: {name: name} })
  setName('')
  }
 
 return(
  <>
    <form onSubmit={handleSubmit}>
      <input type="text" value={name} onChange={e => setName(e.target.value)} />
     </form>
     {todos.map(todo => {
     return <Todo key={todo.id} todo={todo} dispatch={dispatch}/>
     })}
  </>
  )
}
```
