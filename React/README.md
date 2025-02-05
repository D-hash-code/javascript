## Scrimba

Can't recommend highly enough!

[Link to tutorial](https://scrimba.com/learn/learnreact/)

### No backend? No problem.
If you haven't set up your backend just yet and and have an idea as to what the data will look like coming in, in terms of both structure and content, then you can try do something like this?

Use a .js file with an array like [this](JokesData.js) and then import it using

```javascript
import jokesData from "./JokesData";
```
jokesData is a JS Object like the data coming in will probably be


### Leveraging Maps and Components in React

[Good Maps to Components Chapter](https://scrimba.com/learn/learnreact/project-map-experiences-data-into-components-co0704006bcf75aae48fb04c3)


Like a for loop? But handier

```javascript
const jokesElements = jokesData.map(joke => {
        return <JokeComponent />
    })
```
NOTE: Maps Need a `key` prop when used for rendering Components

### Questions from Bob about `.maps()`

**1. What does the `.map()` array method do?**

Returns a new array. Whatever gets returned from the callback
function provided is placed at the same index in the new array.
Usually we take the items from the original array and modify them
in some way.


**2. What do we usually use `.map()` for in React?**

Convert an array of raw data into an array of JSX elements
that can be displayed on the page.


**3. Why is using `.map()` better than just creating the components
   manually by typing them out?**

It makes our code more "self-sustaining" - not requiring
additional changes whenever the data changes.


### Conditional rendering

[Conditional Rendering Chapter](https://scrimba.com/learn/learnreact/project-sold-out-badge-cod6a41078bdec8db3c39513b)

The term refers to when we will only sometimes render a part of a page. In the below code block, every part of the component will get rendered every time a component is called.

```javascript
import React from "react"

export default function Card(props) {
    return (
        <div className="card">
            <img src={`../images/${props.img}`} className="card--image" />
            <div className="card--stats">
                <img src="../images/star.png" className="card--star" />
                <span>{props.rating}</span>
                <span className="gray">({props.reviewCount}) • </span>
                <span className="gray">{props.location}</span>
            </div>
            <p className="card--title">{props.title}</p>
            <p className="card--price"><span className="bold">From ${props.price}</span> / person</p>
        </div>
    )
}
```
Suppose we wish to render a small graphical component with some text if the value of "counter" is greater than 0.

```javascript
{counter>0 && <div>Counter Value Greater than Zero</div>}
```
Including {} inside the JSX actually escapes JSX and everything inside the curly braces is javascript. Now inside the curly braces we can use javascript to check if counter is greater than zero. If it is then the rest of the contents of the curly braces will process, i.e. it will render. Otherwise not.

### Pass objects as Props

[Pass objects as props chapter](https://scrimba.com/learn/learnreact/project-pass-object-as-props-cod6f4e56bca6a67caca77684)

So instead of passing through
```javascript
<Card
    key={item.id}
    img={item.coverImg}
    rating={item.stats.rating}
    reviewCount={item.stats.reviewCount}
    location={item.location}
    title={item.title}
    price={item.price}
    openSpots={item.openSpots}
/>
```

We can simply pass through. Note we need to keep the key prop.
```javascript
<Card
    key={item.id}
    item={item}
/>
```

Having made this change we need to go into the component definition and make some corresponding adjustments there

#### Spreads

In the wild, people will shorten this...
```javascript
 const cards = data.map(item => {
     return (
         <Card
             key={item.id}
             id={item.id}
             title={item.title}
             description={item.description}
             
         />
     )
 })        
    
```

... to this
```javascript
 const cards = data.map(item => {
     return (
         <Card
             key={item.id}
             {...item}
             
         />
     )
 })   
```

Read about it [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax#spread_in_object_literals)

While this makes things more succint in the component. E.g. we don't need to write `props.item.stats.reviewCount`, we can instead now write `props.stats.reviewCount`. This method can create obscurity because we sometimes won't know what is coming from the data source.


### Notes from Building a Meme Generator

- 1 rem == 16 px preferable to use rem for fonts for some reason?
- Use flex box for a strip like layout where everything is on a single line
- Why use padding? 
- When there are components dependent on states we need to make considerations for passing state information across to the components
- In styling the meme generator body/main the process used
  - write out the html objects
  - if using grid, decide how the page should be broken down (in terms of sections) and create the grid container html and style
  - put the grid information in the html objects corresponding style
  - add padding and margins as necessary. in the tutorial they placed a gap element in the grid parent container style and the padding component in the main style component
  - adjust borders
  - adjust fonts (not always necessary if predefined)

#### On building a Reactive Web Application

> the difference between a static and dynamic webpage is the ability for a user to interact with the page. In order for a user to interact with the page we have to be listening to various "events" on the page and reacting when those events happen.

In the case of the meme generator
- as soon as the app loads for the very first time (event), it is going to make an api call to an api called image flip which returns an array of 100 meme images.
- Clicking the get a new meme image button (event), will randomly choose one of those images from the array that got returned to us.
- We need to add an "event listener" to the button so that we can run some logic when the button is hit

### Event Listeners

[Event Listeners Chapter](https://scrimba.com/learn/learnreact/event-listeners-co45a4eba8c0ba3e8ba7df31b)

There are two main ways to add event listeners to a vanilla js program.

```javascript
button.addEventListener("click", function() {
    return ...
})
```

or within the html we have something like
```javascript
<div onclick="myFunction()" id="root"></div>
```
where myFunction() points to some js function. This second way is more similar to how event listeners are added through React.

Suppose we want to log something on the console when a certain button is clicked. In the jsx we add
```javascript
<button onClick={function() {}}>Click me</button>
```
Notice the capital C in onClick. This is because we are accessing the dom properties of the object, which you can see if you do getDocumentById and access the properties. Basically, instead of using lower case as is typical in standard html, we use camel casing `onclick -> onClick`.

Another thing is that because we are in jsx, instead of putting in a string we can just write the function through curly braces, or call the function from the braces.

#### A quick unpleasant GOTCHA
What is wrong with the following (as it relates to the above desired behaviour)?

```javascript
export default function App() {
    var counter = 0
    function handleClick() {
        console.log("I was clicked!")
    }
    
    return (
        <div className="container">
            <button onClick={handleClick()}>Click me</button>
        </div>
    )
}
```

You, like myself, may be tricked into thinking that you can simply place the function like `handleClick()` and it would work fine. But when you do that, on rendering the page it runs the function handleClick, and when you click the button it does nothing. Particularly, when it reads that line it runs the function.

Instead, we need to pass the function as a value (see below), so that react can add that function as the event handler in case the button is ever clicked.

```javascript
export default function App() {
    var counter = 0
    function handleClick() {
        console.log("I was clicked!")
    }
    
    return (
        <div className="container">
            <button onClick={handleClick}>Click me</button>
        </div>
    )
}
```

[Here is a full list of events that react supports](https://reactjs.org/docs/events.html#mouse-events)

Mouse events take up about 95% of the events that web applications listen for.

### Starting to think about APIs, the fun stuff

[Link to API chapter](https://scrimba.com/learn/learnreact/project-get-random-meme-co0d240b0b92838697b8749a1)

Here is a way to get a random element from an array 
```javascript
var item = array[Math.floor(Math.random()*array.length)];
```

Object destructuring! This is cool!

```javascript
// Given that each element in the memesArray has a url key then

const url = memesArray[randomNumber].url

// is equivalent to 

const {url} = memesArray[randomNumber]

```

If at the beginning of rendering a page a certain variable isn't defined then react won't render it on the page. When that variable is later set, either through the click of a button or some interaction we need to make some changes so that react can appropriately react.


### Motivating States, Getting Interactive

[Our current conundrum](https://scrimba.com/learn/learnreact/our-current-conundrum-co53a4b68be61be4a8e646607)

The great mystery: when to use semicolons?

```javascript
function App() {
    const thingsArray = ["Thing 1", "Thing 2"]
    const thingsElements = thingsArray.map(thing => <p key={thing}>{thing}</p>)
    
    function newElement() {
        const newItem = "Thing " + (thingsArray.length + 1);
        thingsArray.push(newItem);
        console.log(thingsArray);
        return null
    }
    
    return (
        <div>
            <button onClick={newElement}>Add Item</button>
            {thingsElements}
        </div>
    )
}

ReactDOM.render(<App />, document.getElementById('root'));
```

A common error causer is forgetting to preempt things with const/var etc. 

React is not looking at local arrays that are just saved within a component to determine whether or not something should get re-rendered. Or if the return should run again with an updated value for things elements. No matter what you do to change thingsArray after render its not automatically going to change thingsElements.

React sort of freezes thingsArray in memory when it renders the page.


Typically, for Vanilla JS you need to find out which component or area needs to get rerendered for this change to come into effect on the page. But the advantage of react is that it is declarative, in that we can just focus on making sure that the data update is correct, and react will handle the rest.

For this to work, we need to access something called react state. State will allow us to Hook into the component and make it so that whenever we update our state (which is really just values that we are saving inside the component) it makes it so that react will update the user interface based on any changes that happen to those values being saved in state. 


and VOILA...

```javascript
import React from 'react';
import ReactDOM from 'react-dom';

function App() {
    const [things, setThings] = React.useState(["Thing 1", "Thing 2"])
    
    function addItem() {
        const newThingText = `Thing ${things.length + 1}`
        setThings(prevState => [...prevState, newThingText])
    }
    
    const thingsElements = things.map(thing => <p key={thing}>{thing}</p>)
    
    return (
        <div>
            <button onClick={addItem}>Add Item</button>
            {thingsElements}
        </div>
    )
}

ReactDOM.render(<App />, document.getElementById('root'));
```


### Using States vs Props

[When to use states vs props](https://scrimba.com/learn/learnreact/props-vs-state-state-cofdc4d4d891c36fc3b0c77fa)

Props are not passed into a function to be reassigned or replaced. That is a huge red flag. If you want to change the value of a prop going into a component you change it at the level of calling the component not inside the component.

On the other hand there will be reasons for you to want to have variables that change or can be different within the component depending on context. E.g. depending on the time of day you display certain information.

**In react values that are created by the function or component are usually handled with state.**


```javascript

function greeting(name) {
    const date = new Date()
    const hours = date.getHours()
    
    let timeOfDay
    if(hours >= 4 && hours < 12) {
        timeOfDay = "morning"
    } else if(hours >= 12 && hours < 17) {
        timeOfDay = "afternoon"
    } else if(hours >= 17 && hours < 20) {
        timeOfDay = "evening"
    } else {
        timeOfDay = "night"
    }
    
    return `Good ${timeOfDay}, ${name}!`
}

console.log(greeting("Bob"))
```

### useState and Array Destructuring

[useState and Array Destructuring](https://scrimba.com/learn/learnreact/usestate-array-destructuring-co70846728c7d60f51fa1997c)

This is more or less how you define a state

```javascript
import React from "react"
import ReactDOM from "react-dom"

export default function App() {
    const [isImportant, func] = React.useState("Yes")
    return (
        <div className="state">
            <h1 className="state--title">Is state important to know?</h1>
            <div className="state--value">
                <h1>{isImportant}</h1>
            </div>
        </div>
    )
}

ReactDOM.render(<App />, document.getElementById("root"))
```

Now, the reason we are given a function from `React.useState()` is for us to use when we want to change the value/data/state, and react will handle those changes accordingly.

Note, for states the `func` is usually named `set`, so in this example we would write `setIsImportant`. And whatever value provided to it is going to be the new version of state. `setIsImportant("No")`

```javascript
import React from "react"

export default function App() {
    const [isImportant, setIsImportant] = React.useState("Yes")

    function handleClick() {
        setIsImportant("No")
    }
    
    return (
        <div className="state">
            <h1 className="state--title">Is state important to know?</h1>
            <div className="state--value" onClick={handleClick}>
                <h1>{isImportant}</h1>
            </div>
        </div>
    )
}
```


A good rule is to declare the handleClick type functions that change the state inside the component. Not exactly sure why but have a hunch.


This technically works but it's not best practice to use the `count` value inside the `setCount` function

```javascript
import React from "react"

export default function App() {
    const [count, setCount] = React.useState(0)
    
    function add() {
        setCount(count + 1)
    }
    
    function subtract() {
        setCount(count - 1)
    }
    
    return (
        <div className="counter">
            <button className="counter--minus" onClick={subtract}>–</button>
            <div className="counter--count">
                <h1>{count}</h1>
            </div>
            <button className="counter--plus" onClick={add}>+</button>
        </div>
    )
}
```

Let's find out why and what to do about it.

### useState - Changing state with a Callback function

[Changing state with a callback function](https://scrimba.com/learn/learnreact/usestate-changing-state-with-a-callback-function-cof9245f4a914e8aaf080c783)

Understanding why the following below is a better way to update a state using the previous state value requires a deeper understanding of how state works. 

By default, when we call the setCount function with a callback on the inside, the default argument passed in is the previous state

```javascript
import React from "react"

export default function App() {
    const [count, setCount] = React.useState(0)
    
    function add() {
        setCount(function(oldValue) {
            return oldValue + 1
        })
    }
    
    function subtract() {
        setCount(count - 1)
    }
    
    return (
        <div className="counter">
            <button className="counter--minus" onClick={subtract}>–</button>
            <div className="counter--count">
                <h1>{count}</h1>
            </div>
            <button className="counter--plus" onClick={add}>+</button>
        </div>
    )
}
```

We can shorten this a bit by replacing the callback part with an arrow thingy

```javascript
function add() {
    setCount(oldValue => oldValue + 1)
}
```
Bob further recommends this
```javascript
function add() {
    setCount(prevCount => prevCount + 1)
}
```
Here it is in Bob's words

> Note: if you ever need the old value of state to help you determine the new value of state, you should pass a callback function to your state setter function instead of using  state directly. This callback function will receive the old value of state as its parameter, which you can then use to determine your new value of state.


An example of a simple useState usage
```javascript
import React from "react"
import memesData from "../memesData.js"

export default function Meme() {
    const [memeImage, setMemeImage] = React.useState("")
    
    function getMemeImage() {
        const memesArray = memesData.data.memes
        const randomNumber = Math.floor(Math.random() * memesArray.length)
        setMemeImage(memesArray[randomNumber].url)
        
    }
    
    return (
        <main>
            <div className="form">
                <input 
                    type="text"
                    placeholder="Top text"
                    className="form--input"
                />
                <input 
                    type="text"
                    placeholder="Bottom text"
                    className="form--input"
                />
                <button 
                    className="form--button"
                    onClick={getMemeImage}
                >
                    Get a new meme image 🖼
                </button>
            </div>
            <img src={memeImage} className="meme--image" />
        </main>
    )
}
```

### Ternary's and more state stuff

[ternar's and state stuff](https://scrimba.com/learn/learnreact/challenge-flipping-state-back-and-forth-co4674229b54cd8335c75e54d)



```javascript
import React from "react"

export default function App() {
    const [isGoingOut, setIsGoingOut] = React.useState(true)

    function changeMind() {
        setIsGoingOut(prevState => !prevState)
    }
    
    return (
        <div className="state">
            <h1 className="state--title">Do I feel like going out tonight?</h1>
            <div onClick={changeMind} className="state--value">
                <h1>{isGoingOut ? "Yes" : "No"}</h1>
            </div>
        </div>
    )
}
```

### More examples
The `[...prevThingsArray, newElement]` go me. Keeping it here so I can reference it when needed.

Some other things is the simple `.length` and how to form strings in javascript.


```javascript
import React from 'react';
import ReactDOM from 'react-dom';

function App() {

    const [thingsArray, setThingsArray] = React.useState(["Thing 1", "Thing 2"])
    
    function addItem() {
        setThingsArray(prevThingsArray => {
            return [...prevThingsArray, `Thing ${prevThingsArray.length + 1}`]
        })
    }
    
    const thingsElements = thingsArray.map(thing => <p key={thing}>{thing}</p>)
    
    return (
        <div>
            <button onClick={addItem}>Add Item</button>
            {thingsElements}
        </div>
    )
}

ReactDOM.render(<App />, document.getElementById('root'));
```

### Complex State - working with object state items

```javascript
const [contact, setContact] = React.useState({
    firstName: "John",
    lastName: "Doe",
    phone: "+1 (719) 555-1212",
    email: "itsmyrealname@example.com",
    isFavorite: true
})

function toggleFavorite() {
    setContact(prevContact => {
        return {
            ...prevContact,
            isFavorite: !prevContact.isFavorite
        }
    })
}
```

use the ... operator to spread out the object.


## Articles

### React Hooks

[Intro to React Hooks - American Express Technology](https://americanexpress.io/hooks-intro/)

> Remember, this is the logic for keeping the current count in state, and for incrementing and decrementing the count. It doesn’t render anything by itself—the render prop does that—and yet we still treat it as a component (i.e., we render it with <Counter />).

The idea that the /logic for handling the state values/ is included in the part where we render the component doesn’t make sense

> Instead of the logic calling something to render, what if we started with what you want to render, and have that call—or use—the logic to get the data that it needs? That’s what hooks are all about.


When you want to use a hook 
> It is worth noting that instead of passing an initial value, you may pass a function. If you do, useState will only call it once to compute the initial value.

```javascript
const someExpensiveProcedure = () => {
  let results;
  for (let i = 0; i < 10000000; i++) {
    // do someething with results
  }
  return results;
};

const [value, setValue] = useState(someExpensiveProcedure);
 
```



I always wondered why and when they increment the version

> In fact, if you look at this from the standpoint of semantic versioning, 16.8.0 means that there are no breaking changes. That is important. If hooks came out in something like 17.0.0, we might have cause for alarm.



## Questions
* what are render props?
	* The term “render prop” refers to *a technique for sharing code between React components using a prop whose value is a function*
* what are class components? Is that just a reference to react components? Why would hooks replace them?


#### This makes no sense to me 😂
> Performance should also be a consideration when writing hooks. In my useCounter above, the reference to increment and decrement functions will change on each render. This is becasue they are created and returned as arrow functions. This may cause your navigation controls to render unnecessarily.
> If rendering performance is a concern, the solution is—you guessed it—another hook. React provides a useCallback hook for just this reason. We can wrap our callback functions in useCallback and React will memoize them, assuring** that they point to the same function each time.
* what do you mean that the reference to increment and decrement functions will change on each render? Does that mean they 

Basically do this
```javascript
const useCounter = initialCount => {
  const [count, setCount] = useState(initialCount);
  const increment = useCallback(() => setCount(currentCount => currentCount + 1), [setCount]);
  const decrement = useCallback(() => setCount(currentCount => currentCount - 1), [setCount]);

  return {
    count,
    increment,
    decrement,
  };
};
```

Instead of this

```javascript
import { useState } from 'react';

const useCounter = initialCount => {
  const [count, setCount] = useState(initialCount);

  return {
    count,
    increment: () => setCount(currentCount => currentCount + 1),
    decrement: () => setCount(currentCount => currentCount - 1),
  };
};
export default useCounter;
```




