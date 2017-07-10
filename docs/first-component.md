## First Component

Now, during the setup, we really did not create our own React Component, we invoked a built in component. `<h1>Hello React</h1>`

> Notice I used the word invoked when referring to the component markup. A component is just a function or class that returns a component. So when we use JSX to declare a component, we are basically invoking the component. I prefer to think of it as calling a function.

You will also noticed, built in components are lowercase and all defined components are capitalized.

### Lets create a component.

It is common convention to have one component per file. So lets create a new file called `app.js`

``` js
// always import React for you component
// JSX needs React to createElements
import React from 'react'

const App = props => {
  return (
    <div>My First Component</div>
  )
}

export default App
```

There are two ways to create React Component, the above way is called a stateless functional component. It is just a function that returns a component. The other way is called a stateful component. And it looks like this:

```
class App extends React.Component {
  render() {
    return (
      <div>My First Component</div>
    )
  }
}
```

> You may notice JavaScript always has several ways to do the same functionality.

In this case, the class code, gives you the ability to manage state inside the component itself, but since we will be using redux to manage state, most of our components can be simple functions.

You can read more about React Components [here](https://facebook.github.io/react/docs/components-and-props.html)

### App Component

Now that we created our simple App component, lets add it to the `main.js`.

We want to replace the `<h1>Hello React</h1>` with our `App` Component, but we also need to import it.

So our `main.js` should look like this after the changes:

``` js
import React from 'react'
import ReactDOM from 'react-dom'

import { Provider } from 'react-redux'
import store from './store'

import App from './app'

ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>, 
  document.getElementById('app')
)
```

And now when you view the app using the show link, you should see `My First Component`

---

[Menu](./?path=README.md:1:0)
