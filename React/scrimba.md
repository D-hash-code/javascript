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
Like a for loop? But handier

```javascript
const jokesElements = jokesData.map(joke => {
        return <JokeComponent />
    })
```

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
