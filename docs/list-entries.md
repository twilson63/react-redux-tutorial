## List Entries

Ok, lets show some data, in this exercise we are going to connect to a list of error log documents from our redux store and display them in our app component.

We will be using some thing you may not be very familiar with at this point, but it should start to make sense as we move further down the tutorial.

We are going to attach this step in interations, the first iteration is to paint some data to the screen as quickly as possible.

For this, we will take a list of data, and transform it into a list of components. A perfect function to take a list of data and transform it into a list of components is the `map` function. Now we could use the built in Array.map, and that would work fine, but I would like to introduce `Ramda`, which has a `map` function. 

### Why Ramda?

Ramda provides small functional helper methods that are all composable, curried and are designed to work together.

[Ramda Map](http://ramdajs.com/docs/#map)

Basically, the ramda map function, takes a function that will transform each value, and a list of items.

In our case, we want to transform a list of documents, into a list of react components.

```
<ul>
{ map(doc => <li>{doc.name}</li>, [{name: 'Error 1'}, {name: 'Error 2'}]) }
</ul>
```

The map function, iterates through each item in the array and returns a new array with the transformed result returned in the function.

### Lets build our list render process

In `app.js` we want to modify it to render a list of line items.

``` js
import React from 'react'

import R from 'ramda'
const { map } = R

const App = props => {
  return (
    <div>
      <header>
        <h1>Error Log</h1>
      </header>
     <main>
      <ul>
        { map(doc => <li>{doc.name}</li>, [{name: 'Error 1'}, {name: 'Error 2'}]) }
      </ul>
     </main>
    </div>
  )
}

export default App

```

So inside the `<ul>` you may notice the curly braces, when used in side JSX, it represents an expression, or javascript statement, that returns either a component, list of components or null.

### Connect to Redux

Now that we have the presentation part of the step working, we need to walk down to getting the data from a database, the first stop is the redux store. We need to create a new reducer to hold all of our entries.

In our store.js file lets create a new function:

```
const SET_ENTRIES = 'SET_ENTRIES'
function entries (state=[{name: 'Error 1a'}, {name: 'Error 2a'}], action) {
  switch (action.type) {
    case SET_ENTRIES:
      return action.payload
    default:
      return state
  }
}
```

Now we need to add the entries node to our combineReducers Object

```
const store = createStore(
  combineReducers({
    app,
    entries
  }),
  applyMiddleware(thunk)
)
```

Now we can link our store state to our app using the connect function from `react-redux`.

In our `app.js` we want to import `{connect}` from `react-redux` then we need to define a new function called `mapStateToProps`. This is where we will take the state from the redux store and add it to the component props.

```
import { connect } from 'react-redux'

...

function mapStateToProps(state) {
  return {
    entries: state.entries
  }
}
```

Finally, we need to use the connect method to wrap the component.

```
export default connect(mapStateToProps)(App)
```

Once you have these steps complete and your app debugged, make the following change in the App function:

```
<ul>
  { map(li, props.entries)}
</ul>
```

At this point you should be seeing your data show from your redux store! 

Congrats!

But we are not done, we want our data to come from the database to our redux store then to our react component.

```
Database -> Store -> Component
```

### Connect to Database

In order to connect to the database when the application start, we want to import our db module in to our store.js file and then call the `allDocs` function and dispatch the results to the redux store.

#### Dispatch

Dispatch is a redux function that is used to send an `action` to the the redux store. An action consists of a `type` and a `payload`. Each reducer can invoke logic based on the `action.type` and use the `action.payload` to help peform logic operations.

In this case, we want to dispatch all of the docs in the database to our redux store, via type SET_ENTRIES.

``` js
import { allDocs } from './db'

... after store is defined

// load docs from db.
allDocs().then(docs => store.dispatch({type: SET_ENTRIES, payload: docs}))
```

If you did this correctly, we should see our default documents go away!

Great Job!!!!

Now, lets seed the database with some dummy documents.

Open up the `db.js` file and at the end of the file add the following:

``` js
db.bulkDocs([
  { _id: 1, name: 'Foo 1'},
  { _id: 2, name: 'Bar 2'}
])
  .catch(err => console.log('docs already loaded, comment me out!'))
```

After the statement has run and you can see Foo 1 and Bar 2 in your list, comment out the command.

Congrats! You have connected your Data to your State to your View.

Whew, that is a lot of stuff going on, and you probaly don't fully understand all of it just yet, and that is ok. We are incrementally learning, and if you keep practicing the process these pieces will start to sink in.

Just to review 

Part 1 - Showing data

We used a function called map to transform a collection of objects into a collection of components, mainly `li` components. Then we used the `{}` in the render function to indicate that a javascript statement needed to be processed and the results needed to be placed in this area of the template.

Part 2 - Getting data from the redux store

In part 2 we used the `connect` function from react-redux module that enabled us to see the redux state store and map the state to props on the component. By creating a function called `mapStateToProps` and then attaching that function using connect to wrap around our app component, we were able to grab the redux state and apply it to the react component props.

In the redux store, we created a new reducer for `entries` and set the default collection to the entries reducer as a couple of fake entries. Once we completed this, we should be able to verify our work by changing the map statement we completed in part 1 to use the `props.entries` property to confirm we are painting data from the redux store.

Part 3 - Connect to a database

Now that we have data from our redux store painting our components, we need to get the data from our database to our redux store. Here we learned about the `dispatch` method and how to use it to our advantage.

This was a big step, but it was worth it, now we can see data from our database show on our screen, pretty cool!!!!

---

[Menu](./?path=README.md:1:0)
