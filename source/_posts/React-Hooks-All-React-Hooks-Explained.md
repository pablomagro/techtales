---
title: React Hooks - Some React Hooks Explained
date: 2023-04-15 09:31:01
categories:
  - React
tags:
  - Hooks
---

# [Built-in React Hooks](https://react.dev/reference/react)

Hooks are a new addition in [React 16.8](https://legacy.reactjs.org/blog/2019/02/06/react-v16.8.0.html). They let you use state and other React features without writing a class. Tey are build-in in the chore of React.

One of the benefits of React is that it does for you, if you determine some sort of system to manage the state of the application

Changing the state of the application and as you change the state of the application the webpage itself re-renders automatically to show the new values.

# List of Hooks

1. [State Hooks](#state-hooks)
   1. [useState](#useState)
   1. [useReducer](#useReducer)
1. [Effect Hooks](#Effect-Hooks)
   1. [useEffect](#useEffect)
   1. [useLayoutEffect](#useLayoutEffect)
1. [Ref Hooks](#Ref-Hooks)
   1. [useRef](#useRef)
1. [Context Hooks](#Context-Hooks)
   1. [useContext](#useContext)
1. [Performance Hooks](performance-hooks)
   1. [useMemo](#useMemo)
   1. [useCallback](#useCallback)
   1. [useDeferredValue](#useDeferredValue)
1. [Other Hooks](#other-hooks)
   1. [useDebugValue](#useDebugValue)


## [State Hooks](https://react.dev/reference/react#state-hooks)<a id="state-hooks"></a>

To add state to a component, use one of these Hooks:

- ``useState`` declares a state variable that you can update directly.

- ``useReducer`` declares a state variable with the update logic inside a reducer function


### [useState](https://react.dev/reference/react/useState)<a id="useState"></a>

useState is a React Hook that lets you add a state variable to your `component`.

    When data changes re-render de UI

#### An example of using useState

```JavaScript
// Reactive value, setter
const [state, setState] = useState(initialState);


// A function example
function UseStateEffect() {
  const [data, setData] = useState("");
  const [inputValue, setInputValue] = useState("");

  let onChange = (event) => {
    const newValue = event.target.value
    setInputValue(newValue);
  }

  useEffect(() => {
    getDummyData(async () => {
      const { data} = await axios.get("https://jsonplaceholder.typicode.com/comments")
      setData(response.data[0].email);
      console.log("API WAS CALLED");
    })
  }, []);

  return (
    <div>
      <input placeholder = "Enter something..." onChange={onChange} />
      {inputValue}
      {/* <h1>{data}</h1> */}
    </div>
  );
}

export default UseStateEffect;
```

### [useReducer](https://react.dev/reference/react/useReducer)<a id="useReducer"></a>

It's an alternative to the useState, which form me is less cleaner and adding extra complexity. ``I wouldn't use`` `Redux` is more complex rather than use `setState` to manage the state when it grows.

Declares a state variable with the update logic inside a [reducer function](https://react.dev/learn/extracting-state-logic-into-a-reducer).

Call useReducer at the top level of your component to manage its state with a reducer.

#### An example of using useReduce

```JavaScript
// Similar to set state, but a different way to set/manage state using the REDUX pattern.
useReducer(reducer, initialArg, init?)

// An example
const reducer = (state, action) => {
  switch (action.type) {
    case "INCREMENT":
      return { count: state.count + 1, showText: state.showText };
    case "toggleShowText":
      return { count: state.count, showText: !state.showText };
    default:
      return state;
  }
};

const UseReducer = () => {
  const [state, dispatch] = useReducer(reducer, { count: 0, showText: true });

  return (
    <div>
      <h1>{state.count}</h1>
      <button
        onClick={() => {
          dispatch({ type: "INCREMENT" });
          dispatch({ type: "toggleShowText" });
        }}
      >
        Click Here
      </button>

      {state.showText && <p>This is a text</p>}
    </div>
  );
};

```
---

## [Effect Hooks](https://react.dev/reference/react#effect-hooks)<a id="Effect-Hooks"></a>

Effects let a component connect to and synchronize with external systems. This includes dealing with network, browser DOM, animations, widgets written using a different UI library, and other non-React code.

- ``useEffect`` connects a component to an external system.

Effects are an “escape hatch” from the React paradigm. Don’t use Effects to orchestrate the data flow of your application. If you’re not interacting with an external system, [you might not need an Effect](https://react.dev/learn/you-might-not-need-an-effect).

There are two rarely used variations of `useEffect` with differences in timing:

- ``useLayoutEffect`` fires before the browser repaints the screen. You can measure layout here.
- [useInsertionEffect](https://react.dev/reference/react/useInsertionEffect) fires before React makes changes to the DOM. Libraries can insert dynamic CSS here.

### [**useEffect**](https://react.dev/reference/react/useEffect)<a id="useEffect"></a>

``useEffect`` is a React Hook that lets you [synchronize a component with an external system](https://react.dev/learn/synchronizing-with-effects).

      useEffect(setup, dependencies?)

#### An example of using useEffect

Call `useEffect` at the top level of your component to declare an Effect:

```JavaScript
import { useEffect } from 'react';
import { createConnection } from './chat.js';

function ChatRoom({ roomId }) {
  // Reactive value, setter
  const [serverUrl, setServerUrl] = useState('https://localhost:1234');

  useEffect(
    () => {
      // RUN when mounted and when state changes (2).
      // alert("Hello side effect!")
      const connection = createConnection(serverUrl, roomId);
      connection.connect();
      // RUN before the component is removed from the DOM
      return () => {
        connection.disconnect();
      };
    },
    // Array of dependencies, with [] there is no dependencies, it's triggered once.
    // RUN when serverUrl or roomId change.
    [serverUrl, roomId]
  );
  // ...
}
```

## [**useLayoutEffect**](https://react.dev/reference/react/useLayoutEffect)<a id="useLayoutEffect"></a>

<h2 style="color: red; font-weight: bold;">Pitfall:
 <span style="color: black; font-weight: normal;">useLayoutEffect can hurt performance. Prefer  <a href="[Ref-Hooks](https://react.dev/reference/react/useEffect)">useEffect</a> when possible</span>
</h2>

- **Similar** to **useEffect** but
- **RUNS** after render, but before pointing the script.
- **CAUTION** blocks visual updates until your callback is finished.

useLayoutEffect is a version of [useEffect](https://react.dev/reference/react/useEffect) that fires before the browser repaints the screen.

    useLayoutEffect(setup, dependencies?)

#### An example of using useLayoutEffect

Call ``useLayoutEffect`` perform the layout measurements before the browser repaints the screen:

```JavaScript
import React, { useState, useLayoutEffect, useRef } from 'react';

function MyComponent() {
  const [width, setWidth] = useState(0);
  const ref = useRef(null);

  /* ***************************************************************
   * Similar to useEffect, but
   * RUNS after render, but before pointing the script.
   * CAUTION blocks visual updates until your callback is finished
   * *************************************************************** */

  // Use useLayoutEffect to measure the width of the element
  useLayoutEffect(() => {
    if (ref.current) {
      const newWidth = ref.current.getBoundingClientRect().width;
      setWidth(newWidth);
    }
  }, []);

  return (
    <div ref={ref}>
      This element has a width of {width}px.
    </div>
  );
}
```

Note that `useLayoutEffect` should be used sparingly, as it can negatively impact the performance of your application if used excessively or inefficiently. You should only use `useLayoutEffect` when you need to perform a measurement or layout calculation that affects the visual appearance of your application.

- [Reference](https://react.dev/reference/react/useLayoutEffect#reference)
  - [useLayoutEffect(setup, dependencies?)](https://react.dev/reference/react/useLayoutEffect#useinsertioneffect)
- [Usage](https://react.dev/reference/react/useLayoutEffect#usage)
  - [Measuring layout before the browser repaints the screen](https://react.dev/reference/react/useLayoutEffect#measuring-layout-before-the-browser-repaints-the-screen)
- [Troubleshooting](https://react.dev/reference/react/useLayoutEffect#troubleshooting)
  - [I’m getting an error: ”useLayoutEffect does nothing on the server”](https://react.dev/reference/react/useLayoutEffect#im-getting-an-error-uselayouteffect-does-nothing-on-the-server)


## [Ref Hooks](https://react.dev/reference/react#effect-hooks) <a id="Ref-Hooks"></a>

*Refs* let a component [hold some information that isn’t used for rendering,](https://react.dev/learn/referencing-values-with-refs) like a DOM node or a timeout ID. Unlike with state, updating a ref does not re-render your component. Refs are an “escape hatch” from the React paradigm. They are useful when you need to work with non-React systems, such as the built-in browser APIs.

- [useRef](https://react.dev/reference/react/useRef) declares a ref. You can hold any value in it, but most often it’s used to hold a DOM node.
- [useImperativeHandle](https://react.dev/reference/react/useImperativeHandle) lets you customize the ref exposed by your component. This is rarely used.

Easiest way to manipulate and access DOM elements.


### [useRef](https://react.dev/reference/react/useRef)<a id="useRef"></a>

useRef is a React Hook that lets you reference a value that’s not needed for rendering.

      const ref = useRef(initialValue)

#### An example of using useRef
Use the `useRef` hook in a React component to store a reference to a DOM element:

```JavaScript
import React, { useRef } from 'react';

function MyComponent() {
  const inputRef = useRef(null);

  function handleButtonClick() {
    // Focus the input element
    inputRef.current.focus();
  }

  return (
    <div>
      <input type="text" placeholder="Example..." ref={inputRef} />
      <button onClick={handleButtonClick}>Focus input</button>
    </div>
  );
}
```

By using the `useRef` hook to store a reference to the input element, we can avoid the need to rely on DOM queries or selectors to manipulate the input element, which can be slower and less reliable. Instead, we can directly access the input element using the `current` property of the `inputRef` object.

- [Reference](https://react.dev/reference/react/useRef#reference)
  - [useRef(initialValue)](https://react.dev/reference/react/useRef#useref)
- [Usage](https://react.dev/reference/react/useRef#usage)
  - [Referencing a value with a ref](https://react.dev/reference/react/useRef#referencing-a-value-with-a-ref)
  - [Manipulating the DOM with a ref](https://react.dev/reference/react/useRef#manipulating-the-dom-with-a-ref)
  - [Avoiding recreating the ref contents](https://react.dev/reference/react/useRef#avoiding-recreating-the-ref-contents)
- [Troubleshooting](https://react.dev/reference/react/useRef#troubleshooting)
  - [I can’t get a ref to a custom component](https://react.dev/reference/react/useRef#i-cant-get-a-ref-to-a-custom-component)

Creating a some short of to-do application, clear an input file when submitted the value

---

## [Context Hooks](https://react.dev/reference/react#context-hooks) <a name="Context-Hooks"></a>

*Context* lets a component [receive information from distant parents without passing it as props.](https://react.dev/learn/passing-props-to-a-component) For example, your app’s top-level component can pass the current UI theme to all components below, no matter how deep.

- [useContext](https://react.dev/reference/react/useContext) reads and subscribes to a context.

### [**useContext**](https://react.dev/reference/react/useContext) <a name="useContext"></a>

To share value through disconnected components, we can create a context object.

*useContext* is a React Hook that lets you read and subscribe to [context](https://react.dev/learn/passing-data-deeply-with-context) from your component.

      const value = useContext(SomeContext)

#### Examples of using useContext

```JavaScript
import { createContext, useContext } from "react";

const moods = {
  happy: "😄",
  sad: "😒",
}

// To share value through disconnected components, we can create a context object.
// CONTEXT share data without passing props. during the entire component tree.
const MoodContext = createContext(moods)

function MoodEmoji() {
  // Consume value from nearest parent provider.
  const mood = useContext(MoodContext)

  return <p>{ mood.happy }</p>
}

function ReactHooksExplained () {
  // Get the context value.
  const MoodContextValue = useContext(MoodContext);

  return (
    // Create context to scope the mood there,
    // and not need to use pass props down to the child components.
    <MoodContext.Provider value={MoodContextValue}>
      <MoodEmoji />
    </MoodContext.Provider>
  );
}
```
```javascript
const ThemeContext = React.createContext('light');

const Display = () => {
 const theme = useContext(ThemeContext);
 return <div
        style={{
        background: theme === 'dark' ? 'black' : 'papayawhip',
        color: theme === 'dark' ? 'white' : 'palevioletred',
        width: '100%',
        minHeight: '200px'
        }}
    >
        {'The theme here is ' + theme}
    </div>
}
```

- [Reference](https://react.dev/reference/react/useContext#reference)
  - [useContext(SomeContext)](https://react.dev/reference/react/useContext#usecontext)
- [Usage](https://react.dev/reference/react/useContext#usage)
  - [Passing data deeply into the tree](https://react.dev/reference/react/useContext#passing-data-deeply-into-the-tree)
  - [Updating data passed via context](https://react.dev/reference/react/useContext#updating-data-passed-via-context)
  - [Specifying a fallback default value](https://react.dev/reference/react/useContext#specifying-a-fallback-default-value)
  - [Overriding context for a part of the tree](https://react.dev/reference/react/useContext#overriding-context-for-a-part-of-the-tree)
  - [Optimizing re-renders when passing objects and functions](https://react.dev/reference/react/useContext#optimizing-re-renders-when-passing-objects-and-functions)
- [Troubleshooting](https://react.dev/reference/react/useContext#troubleshooting)
  - [My component doesn’t see the value from my provider](https://react.dev/reference/react/useContext#my-component-doesnt-see-the-value-from-my-provider)
  - [I am always getting undefined from my context although the default value is different](https://react.dev/reference/react/useContext#i-am-always-getting-undefined-from-my-context-although-the-default-value-is-different)


## [**Performance Hooks**](https://react.dev/reference/react#performance-hooks) <a name="performance-hooks"></a>

A common way to optimize re-rendering performance is to skip unnecessary work. For example, you can tell React to reuse a cached calculation or to skip a re-render if the data has not changed since the previous render.

To skip calculations and unnecessary re-rendering, use one of these Hooks:

- [useMemo](https://react.dev/reference/react/useMemo) lets you cache the result of an expensive calculation.
- [useCallback](https://react.dev/reference/react/useCallback) lets you cache a function definition before passing it down to an optimized component.

Sometimes, you can’t skip re-rendering because the screen actually needs to update. In that case, you can improve performance by separating blocking updates that must be synchronous (like typing into an input) from non-blocking updates which don’t need to block the user interface (like updating a chart).

To prioritize rendering, use one of these Hooks:

- [useTransition](https://react.dev/reference/react/useTransition) lets you mark a state transition as non-blocking and allow other updates to interrupt it.
- [useDeferredValue](https://react.dev/reference/react/useDeferredValue) lets you defer updating a non-critical part of the UI and let other parts update first.

### [**useMemo**](https://react.dev/reference/react/useMemo) <a name="useMemo"></a>

useMemo is a React Hook that lets you cache the result of a calculation between re-renders.

- **MEMOIZATION**: cache result of function call, to optimize performance
- **CAUTION**: this only used as needed for expensive computations

#### An example of using useMemo

```javascript
// When data changes re-render de UI
const [count, setCount] = useState(0)

// MEMOIZATION: cache result of function call, to optimize performance
// CAUTION: this only used as needed for expensive computations
const expensiveCount = useMemo(() => {
  return count ** 2
}, [count]) // RECOMPUTE: when count changes

return (
    <div className="App">
      <div>{count}</div>
    </div>
)
```

- [Reference](https://react.dev/reference/react/useMemo#reference)
  - [useMemo(calculateValue, dependencies)](https://react.dev/reference/react/useMemo#usememo)
- [Usage](https://react.dev/reference/react/useMemo#usage)
  - [Skipping expensive recalculations](https://react.dev/reference/react/useMemo#skipping-expensive-recalculations)
  - [Skipping re-rendering of components](https://react.dev/reference/react/useMemo#skipping-re-rendering-of-components)
  - [Memoizing a dependency of another Hook](https://react.dev/reference/react/useMemo#memoizing-a-dependency-of-another-hook)
  - [Memoizing a function](https://react.dev/reference/react/useMemo#memoizing-a-function)
- [Troubleshooting](https://react.dev/reference/react/useMemo#troubleshooting)
  - [My calculation runs twice on every re-render](https://react.dev/reference/react/useMemo#my-calculation-runs-twice-on-every-re-render)
  - [My useMemo call is supposed to return an object, but returns undefined](https://react.dev/reference/react/useMemo#my-usememo-call-is-supposed-to-return-an-object-but-returns-undefined)
  - [Every time my component renders, the calculation in useMemo re-runs](https://react.dev/reference/react/useMemo#every-time-my-component-renders-the-calculation-in-usememo-re-runs)
  - [I need to call useMemo for each list item in a loop, but it’s not allowed](https://react.dev/reference/react/useMemo#i-need-to-call-usememo-for-each-list-item-in-a-loop-but-its-not-allowed)

### [**useCallback**](https://react.dev/reference/react/useCallback) <a name="useCallback"></a>
useCallback is a React Hook that lets you cache a function definition between re-renders.

#### An example of useCallback
In this example, the `ChildComponent` receives the `onClick` prop from the `ParentComponent` and uses it to handle a click event on a button element. Because the `onClick` prop is a memoized callback function, the `ChildComponent` can safely use it without needing to worry about unnecessary re-renders due to changes in the function reference.

```javascript
// Maybe we want to memoize the function, passing the function to multiple child components,
// especially with big lists, wrapping the function with avoid unnecessary re-rendering in the child components
// because is using always the same function object.

import React, { useState, useCallback } from 'react';
import ChildComponent from './ChildComponent';

function ParentComponent() {
  const [count, setCount] = useState(0);

  // Define a memoized callback function using the useCallback hook
  const handleClick = useCallback(() => {
    setCount(prevCount => prevCount + 1);
  }, []);

  return (
    <div>
      <p>Count: {count}</p>
      <ChildComponent onClick={handleClick} />
    </div>
  );
}

function ChildComponent({ onClick }) {
  return (
    <button onClick={onClick}>
      Click me!
    </button>
  );
}
```

- [Reference](https://react.dev/reference/react/useCallback#reference)
  - [useCallback(fn, dependencies)](https://react.dev/reference/react/useCallback#usecallback)
- [Usage](https://react.dev/reference/react/useCallback#usage)
  - [Skipping re-rendering of components](https://react.dev/reference/react/useCallback#skipping-re-rendering-of-components)
  - [Updating state from a memoized callback](https://react.dev/reference/react/useCallback#updating-state-from-a-memoized-callback)
  - [Preventing an Effect from firing too often](https://react.dev/reference/react/useCallback#preventing-an-effect-from-firing-too-often)
  - [Optimizing a custom Hook](https://react.dev/reference/react/useCallback#optimizing-a-custom-hook)
- [Troubleshooting](https://react.dev/reference/react/useCallback#troubleshooting)
  - [Every time my component renders, useCallback returns a different function](https://react.dev/reference/react/useCallback#every-time-my-component-renders-usecallback-returns-a-different-function)
  - [I need to call useCallback for each list item in a loop, but it’s not allowed](https://react.dev/reference/react/useCallback#i-need-to-call-usememo-for-each-list-item-in-a-loop-but-its-not-allowed)

### [**useDeferredValue**](https://react.dev/reference/react/useDeferredValue) <a name="useDeferredValue"></a>

The `useDeferredValue` Hook is a new addition to React 18 and it lets you defer updating a part of the UI.

      const deferredValue = useDeferredValue(value)

`useDeferredValue` allows you to defer the rendering of a value until a future point in time, which can be incredibly useful in situations where you want to avoid unnecessary rendering.

```javascript
const [valueToDefer, setValueToDefer] = useState("")
const deferredValue = useDeferredValue(valueToDefer)

return (
  <p>{deferredValue}</p>
  )
```

By using the `useDeferredValue` Hook, you can avoid this problem by deferring the rendering of the search results until the user stops typing. This is similar to how *debouncing* works; it can dramatically improve performance.

The following example shows how to use the `useDeferredValue` Hook to simulate a debouncing pattern retrieving Star War's characters names.

```javascript
import { useDeferredValue, useEffect, useState } from "react"

function UseDeferredHook() {
  const [searchQuery, setSearchQuery] = useState('')
  const deferredSearchQuery = useDeferredValue(searchQuery)
  const [resultQuery, setResultQuery] = useState([])

  useEffect(() => {
    async function fetchPeople() {
      if (!searchQuery) {
        setResultQuery([])
        return
      }

      const response = await fetch(`https://swapi.dev/api/people/?search=${deferredSearchQuery}`)
      const { results } = await response.json()
      setResultQuery(results)
    }

    fetchPeople()
  // eslint-disable-next-line react-hooks/exhaustive-deps
  }, [deferredSearchQuery])

  function handleOnChange(event: any) {
    setSearchQuery(event.target.value)
  }

  return (
    <div>
      <input type="input" placeholder="Type a character" value={searchQuery} onChange={handleOnChange} />
      <ul>
        {resultQuery && (resultQuery.map((person : any) => (
          <li key={person.name}>{person.name}</li>
        )))}
      </ul>
    </div>
  )
}

export default UseDeferredHook
```

In this example, it's using the `useState` hook to manage the `searchQuery` state, which holds the user's search input. We're also using the `useDeferredValue` hook to create a `deferredSearchQuery` variable, which we pass to the Star Wars API search endpoint after a 1 second delay.

- [Reference](https://react.dev/reference/react/useDeferredValue#reference)
  - [useDeferredValue(value)](https://react.dev/reference/react/useDeferredValue#usedeferredvalue)
- [Usage](https://react.dev/reference/react/useDeferredValue#usage)
  - [Showing stale content while fresh content is
        > loading](https://react.dev/reference/react/useDeferredValue#showing-stale-content-while-fresh-content-is-loading)
  - [Indicating that the content is
        > stale](https://react.dev/reference/react/useDeferredValue#indicating-that-the-content-is-stale)
  - [Deferring re-rendering for a part of the
        > UI](https://react.dev/reference/react/useDeferredValue#deferring-re-rendering-for-a-part-of-the-ui)

---

## **Other Hooks** <a name="other-hooks"></a>
These [Hooks]((https://react.dev/reference/react#other-hooks)) are mostly useful to library authors and aren’t commonly used in the application code.

- [useDebugValue](https://react.dev/reference/react/useDebugValue) lets you customize the label React DevTools displays for your custom Hook.
- [useId](https://react.dev/reference/react/useId) lets a component associate a unique ID with itself. Typically used with accessibility APIs.
- [useSyncExternalStore](https://react.dev/reference/react/useSyncExternalStore) lets a component subscribe to an external store.

### [**useDebugValue**](https://react.dev/reference/react/useDebugValue) <a name="useDebugValue"></a>
useDebugValue is a React Hook that lets you add a label to a custom Hook in [React DevTools.](https://react.dev/learn/react-developer-tools)

    useDebugValue(value, format?)

#### An example of using useDebugValue

```javascript
// Use in multiple components.
function useDisplayName() {
  const [displayName, setDisplayName] = useState<string>();

  useEffect(() => {
    const data = fetchFromDatabase(props.userId);
    setDisplayName(data.id);
  }, []);

  useDebugValue(displayName ?? 'loading...')

  return displayName;
}
```

- [Reference](https://react.dev/reference/react/useDebugValue#reference)
  - [useDebugValue(value, format?)](https://react.dev/reference/react/useDebugValue#usedebugvalue)
- [Usage](https://react.dev/reference/react/useDebugValue#usage)
  - [Adding a label to a custom Hook](https://react.dev/reference/react/useDebugValue#adding-a-label-to-a-custom-hook)
  - [Deferring formatting of a debug value](https://react.dev/reference/react/useDebugValue#deferring-formatting-of-a-debug-value)

