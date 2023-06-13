---
title: "Let's hook up with React Hooks!"
seoTitle: "Hooking up with react-hooks!"
seoDescription: "Learn react hooks simply without worrying about any complications. This article includes useState useEffect useContext useReducer useRef useLayoutEffect"
datePublished: Sat Sep 03 2022 19:50:52 GMT+0000 (Coordinated Universal Time)
cuid: cl7mblevw020dgznvbwxg6bs9
slug: react-hooks
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1662234316383/br3-JF3z0.png
tags: react-router, javascript, web-development, reactjs, reacthooks

---


Let's hook up with React Hooks!

Hooks improved the development experience because of simpler code & similar functionalities as compared to class-based components. After V16.8 hooks were introduced and now we can use just functional components which were also loved by the community.


![React hooks class based components functional components](https://cdn.hashnode.com/res/hashnode/image/upload/v1662232750609/aC054NT0Q.jpg align="center")

# **useState Hook** 

useState hook allows to track some state in a functional component. It will update the state everywhere if it's changed. <br>
When values are changed --> Component also rerenders


```javascript
import {useState} from “react”;
function FirstHook() {
  //Declaration : returns array of 2 el -> state & function to set state {obj destructuring}
  const [ state , setState ] = useState( initialValue );
  //Update state
  function onClick(){
    setState( initialValue+1 );
  }
  //Consume state
  return { state } ;
}
``` 


# **useEffect Hook** 

Perform side effects on functional components. Like, fetch API, setting a subscription, changing the DOM, changing the title of the page... <br>
Replacement of react component lifecycle methods like componentDidMount, componentDidUpdate, componentWillMount with just one useEffect hook!

> useEffect( ()=>{},[ dependency ]  )

```javascript
import { useEffect } from "react";
// -> **No dependency array passed: runs on every render**
	useEffect( ( )=>{
	    //document.title =newState ;
    } )
// -> []  Empty array: runs on first render only when page loads
	useEffect( ( )=>{
	    //document.title =newState ;
    }, [ ] )
// -> [ props , state ]  -> Props or state values passed: runs when args changed
	useEffect( ( )=>{
        //let’s say some eventListener is added here
        //Clean Up function
	    return ()=>{
	    	//remove previously added event listener to free up cache...
        }
    } , [ props , state ] )
``` 
Note: *No dep arr passed* should be used carefully as it might run an infinite loop… 

![useEffect hooks](https://cdn.hashnode.com/res/hashnode/image/upload/v1662232608128/jxQVFFfPs.jpg align="center")





# **useContext** 

To avoid props drilling { passing props into child components again and again } <br>
maintains store globally <br>
Other alternatives --> Redux. <br> <br>

> CONTEXT API ⇒ context + provider + useContext hook

```javascript
// Store :: – src – components – useContext – userContext.jsx 
import {createContext} from “react”;
const AppContext = createContext();
// children ==> <App> 
const AppProvider = ({ children }) => {
const data ={
	Name:”vaibhav”,
	age:23,
};
	return <AppContext.Provider value={data}> { children } </AppContext.Provider>;
};
export {AppContext, AppProvider};
```

```javascript
// Wrap parent component :: – App.js 
import { AppProvider } from “./components/usecontext/userContext”;
<AppProvider>
	<App/>
</AppProvider>
```

```javascript
// – Consume data :: child.jsx   
import {useContext} from “react”;
import {AppContext} from “./components/useContext/userContext”;
const data = useContext(AppContext);
//can use data anywhere now…
```


![react hooks.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1662274945971/JZNTIbTJi.gif align="left")

# **useReducer** 

Similar to useState, **used for state management** but more powerful than useState hook. <br>
Let’s see how it’s more powerful… <br>

***Why useReducer over useState?*** <br>
While using useState hook we need to specify the operation inside setState function, but here we can just pass type and specify at the backend file( reducer.jsx ) what was the exact operation which becomes more convenient when working on big projects… <br>

> Reducer → state & action
> Dispatch will trigger action method of reducer function

```javascript
import reducer from “./reducer.jsx”;
//Declaration
const [ count,dispatch ] = useReducer( reducer , 0 );  
// Consumes – just like setState was used, here dispatch triggers reducer function
dispatch( {type:”INC”} ) 
```
```javascript
//  useReducer – reducer.jsx
const reducer = (state,action) ⇒ {
    if(action.  type === “INC”){
        state++;
    }
    if(action.type === “DEC”){
  	    state–;
    }
    return state;
}
```

#  **useRef** 
Creates a mutable variable that won’t re-render the components. Used to access the DOM element directly
 
```javascript
import useRef from “react”
const count = useRef( 0 );
// count.current can set and use these values
```
```javascript
// Can use useRef in replace of document.getElementbyId by accessing DOM directly…
const inputRef = useRef();
//Can manipulate this inputRef now
inputRef.current.style.backgroundColor = “red”;
<input type=”text” ref={inputRef} />
```

#  **useLayoutEffect**
Similar to useEffect, same syntax <br> 
> useLayoutEffect runs synchronously after a render but before the screen is updated <br>
> useEffect runs asynchronously and after a render is painted leading to data flicker. This is preferred most of the times… <br>


# **useMemo**
Similar to useEffect<br>
Increase performance, optimizations... <br>
To avoid any unnecessary calling of any function which is not even used
> const var_name = use( callBack , [ dependency ] )
This callback can return the value


#  **useCallback**
Similar to useEffect / useMemo but more powerful

> useMemo → return a memoized value
> useCallback → return a memoized function
Memoization → stores values to avoid doing computation again!


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1662230663091/NYx2WlJuc.png align="left")




