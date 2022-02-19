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