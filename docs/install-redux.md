## Installing Redux

Redux is a state management system, that makes it easy to track when your 
state is being modified in your application. Not all apps need redux, but if you are doing some routing and crud management, redux will most likely be a good choice.

Redux is a flux pattern implementation, but instead of having multiple stores, redux just has one store. Redux uses reducers to modify state and notifies any subscriber when the state changes. React wants to be notified when state changes and render the presentation. This approach creates a very explicit uni-directional flow.

We will talk more about Redux as we go through the tutorial, what we need to know now, is that we are going to create a store.js file and import redux functions into the store.js. We need to import three functions from the redux module:

* createStore
* combineReducers
* applyMiddleware

We also need to bring in another module called `redux-thunk`, it is middleware in redux that enables us to make async calls when we dispatch changes to the redux store.

### Create `store.js`

``` js
import { createStore, combineReducers, applyMiddleware } from 'redux'
import thunk from 'redux-thunk'

const store = createStore(
  combineReducers({
    app
  }),
  applyMiddleware(thunk)
)

export default store

// app reducer 
function app (state={title: 'Error Log App'}, action) {
  switch (action.type) {
    default:
      return state
  }
}
```

In our setup, we are only using one reducer for now, but we will add more. A reducer function, is a function that takes an accumulator and a value. In this case the state is the accumulator and the action is the value. Internally, redux calls a reduce function to take the action and apply it it to all the reducers to get a final object as a result, which is the state of the app.

### Attach our Store to our React App

Now that we have created our store, we need to attach it to our React Application. In order to do this, we use a module called `react-redux`. This module contains a component called `Provider` that we need to put as the first component of our application and wrap our app component around it.

In `main.js` lets import both `Provider` and `store` and wrap our `React` component with the `Provider` component.

``` main.js
import React from 'react'
import ReactDOM from 'react-dom'

import { Provider } from 'react-redux'
import store from './store'

ReactDOM.render(<Provider store={store}><h1>Hello React</h1></Provider>, document.getElementById('app'))
```

We are invoking the Provider Component as the root component of the app, and in the Provider component, we are passing our redux store as a `prop`. Now this may be first time you have heard the word prop, but we will will be discussing it throughout the tutorial. 

Basically, with React components, you need to pass data down and get actions up. With props, we can do both, in this case we are passing the store data into our Provider component.

> Verify your app still works, if not look at the above snippets and make sure you are transcribing correctly.

---

[Menu](./?path=README.md:1:0)
