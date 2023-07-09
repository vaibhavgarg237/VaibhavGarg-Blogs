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

Let's hook up with React Hooks! + Lifecycle Methods

Hooks improved the development experience because of simpler code & similar functionalities as compared to class-based components. After V16.8 hooks were introduced, we can now use just functional components that the community also loved. Below you will also find **react lifecycle methods using class-based components with analogies**.

![React hooks class based components functional components](https://cdn.hashnode.com/res/hashnode/image/upload/v1662232750609/aC054NT0Q.jpg align="center")

# **useState Hook**

useState hook allows tracking some states in a functional component. It will update the state everywhere if it's changed.  
When values are changed --&gt; ***Component also rerenders***

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

Perform side effects on functional components. Like, fetch API, setting a subscription, changing the DOM, changing the title of the page...  
Replacement of react component lifecycle methods like componentDidMount, componentDidUpdate, and componentWillUnmount with just one useEffect hook!

***Refer React Lifecycle diagram in case of class components*** - https://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/

**Lifecycle methods in class-based components:**  
\- *constructor: initialize here, to process before the page loads for the first time ( as it is used for initialize states/ variables, bind methods, a functional component can directly do inside the component body )  
\- render: to add JSX ( not used in functional-based component approach)  
\- componentDidMount: component renders for the first time  
\- componentDidUpdate: component renders after the first time*  
*\- componentWillUnmount: component removed*

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688902776682/91e2e360-2798-4445-bdd3-96cb25f0572a.png align="center")

> useEffect( ()=&gt;{},\[ dependency \] )

```javascript
import { useEffect } from "react";
// -> No dependency array passed: runs on every render
	useEffect( ( )=>{
        //[componentDidMount+componentDidUpdate]
	    //document.title =newState ;
    } )
// -> []  Empty array: runs on first render only when page loads 
	useEffect( ( )=>{
        //[componentDidMount]
	    //document.title =newState ;
    }, [ ] )
// -> [ props , state ]  -> Props or state values passed: runs when args changed 
	useEffect( ( )=>{
        // ([componentDidUpdate] with if condition preprops!=currprops)
        //let’s say some eventListener is added here
	    return ()=>{
	        //[componentWillUnmount] Clean Up function
        	//remove previously added event listener to free up cache...
        }
    } , [ props , state ] )
```

Note: *No dep arr passed* should be used carefully as it might run an infinite loop…

![useEffect hooks](https://cdn.hashnode.com/res/hashnode/image/upload/v1662232608128/jxQVFFfPs.jpg align="center")

# **useContext**

To avoid props drilling { passing props into child components again and again }  
maintains store globally  
Other alternatives --&gt; Redux.

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

Similar to useState, **used for state management** but more powerful than useState hook.  
Let’s see how it’s more powerful…

***Why useReducer over useState?***  
While using the useState hook we need to specify the operation inside the setState function, but here we can just pass type and specify at the backend file( reducer.jsx ) what was the actual operation which becomes more convenient when working on big projects…

With useReducer, React will only re-render your component when the reducer function returns a new state object. This can help you to improve the performance of your application. This means let's say in a single function you are using setState for 2 different states, it will render twice, whereas if using useReducer it will render once because it is changed one time.

> Reducer → state & action Dispatch will trigger action method of reducer function

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

# **useRef**

Creates a mutable variable that won’t re-render the components. Used to access the DOM element directly

React uses a virtual DOM to track the state of your components. When you directly manipulate the DOM, you are bypassing React's state management system, which can lead to inconsistencies. UseRef allows you to access the DOM element from within your component, but it does not allow you to modify it directly. This helps to ensure that your component's state is always up-to-date.

To pass ref just like props, lookout for **forwardRef**

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

# **useLayoutEffect**

Similar to useEffect, same syntax. useEffect after render, useLayoutEffect before render

> useLayoutEffect runs synchronously after a render but before the screen is updated  
> useEffect runs asynchronously and after a render is painted leading to data flicker. This is preferred most of the times…

# useMemo (memoization)

Many times while using useEffect, there might be repetitive re-rendering which will lead to calling the same function multiple times when in case that is not even changed. So to avoid this unnecessary computation we can use the useMemo hook when we need to only call this function where its dependencies change, not the unrelated components get re-rendered.

* Similar to useEffect, Increase performance, optimizations...
    
* In this case, our value computed in the first call is memoized for the next time
    
* Memoization → stores values to avoid doing computation again!
    

```javascript
//replace normal function call with below call
const memoizedFxName = useMemo( () => ogFunctionName(data) , [ data ] );
```

# **useCallback**

* Similar to useEffect / useMemo but more powerful
    
* In this case, our callback function not value is memoized for next time
    

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1662230663091/NYx2WlJuc.png align="left")