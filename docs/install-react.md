## Install React

Since we are using getlibs, installing react is very easy.

GetLibs uses babel and npm to do all the heavy lifting for us. If we were not using getlibs, we may want to look at something like `create-react-app` or `next.js` to simplfy the setup of React with WebPack and Babel.

But in our case it is pretty straight forward. All we have to do is the following:

In the main.js page we need to import both `react` and `react-dom`

The import statement is an ES2015 feature and is implemented by transpiling your code down to es5 so 
that browsers can understand it.

You can read more about the `import` statement here:

> [ES2015 Modules](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import)

Here is what our `main.js` should look like with the `import` statements

``` js
import React from 'react'
import ReactDOM from 'react-dom'

```

Once we have our react modules imported, we need to render a react component. A react component using JSX looks like `HTML` but it actually gets transpiled into a javascript function call.

``` js
ReactDOM.render(<h1>Hello React</h1>, document.getElementById('app'))
```

The JSX is the `<h1Hello React</h1>` and the render method is the method that runs the react view and replaces the contents of the div with the id app with the result of the render.

When it gets transpiled, the statement looks like this:

``` js
ReactDOM.render(React.createElement('h1', null, 'Hello React'), document.getElementById('app'))
```

Which may not look too bad at first, but as you add many components that are composed together, the React.createElement can get very noisy.

To read more about JSX -

[Introducing JSX](https://facebook.github.io/react/docs/introducing-jsx.html)

### In Summary

In this exercise we setup React in our test project, our final main.js file should look like the following:

``` js
import React from 'react'
import ReactDOM from 'react-dom'


ReactDOM.render(<h1>Hello React</h1>, document.getElementById('app'))
```

Click on the Show Live Button at the top and see if your browser now says `Hello React`

---

[Menu](./?path=README.md:1:0)