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

