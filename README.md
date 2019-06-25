# React Components

## Objectives
By the end of this, developers should be able to:

* Identify componenents in a design
* Evaluate and write simple JSX
* Explain react components
* Build a simple component

## React App Components

Let's create a new react application named movies.  We can use the command `create-react-app movies`.

Almost all the work we'll do on a React app will be in the `src` directory. This directory contains all our components (both their markup and JavaScript), all our styles, and the layout and structure of application. Here, we have two very important files: `index.js` and `App.js`.

#### index.js

We won't usually modify `index.js`. The purpose of this file is to bundle up our dependencies, and render our `App` component to the DOM. 

```js
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';

ReactDOM.render(<App />, document.getElementById('root'));

// If you want your app to work offline and load faster, you can change
// unregister() to register() below. Note this comes with some pitfalls.
// Learn more about service workers: http://bit.ly/CRA-PWA
serviceWorker.unregister();
```

#### App.js

Our `App` component is the entry point to our application. Any other components (and indeed, anything at all) that we add to our app will be nested inside this App component. In React, all our code and all our markup live in components!

Let's take a look at what's in `App.js`.

```js
import React, { Component } from 'react';
import logo from './logo.svg';
import './App.css';

class App extends Component {
  render() {
    return (
      <div className="App">
        <header className="App-header">
          <img src={logo} className="App-logo" alt="logo" />
          <h1 className="App-title">Welcome to React</h1>
        </header>
        <p className="App-intro">
          To get started, edit <code>src/App.js</code> and save to reload.
        </p>
      </div>
    );
  }
}

export default App;
```

That's a component! It is a class component.  We usually use class components when we need advanced functionality like "state" or "ajax".  For components that just render static HTML, we can define them as arrow functions that return JSX.  Here's what the same component would look like written as a function instead of a class.

```js
const App = () => {
  return (
      <div className="App">
        <header className="App-header">
          <img src={logo} className="App-logo" alt="logo" />
          <h1 className="App-title">Welcome to React</h1>
        </header>
        <p className="App-intro">
          To get started, edit <code>src/App.js</code> and save to reload.
        </p>
      </div>
    );
} 
```

Let's make the `<header>` its own component and the `<p>` its own component as well.  We will then import them into the `App` component.

1.  First we will use a function component 
2.  Then let's refactor them to class componenets

Notice that the outcome is the same since both the function and class component are just rendering JSX.  Later, we will learn how the two styles of components differ.  For today, we will practice using both.

## Building components

### Code along: A Class Component

Create a new file in `src` called `Movie.js`, and add this simple component to
it.

```js
// bring in React and Component from React

import React, { Component } from 'react';

// define our Movie component
class Movie extends Component {
  // what should the component render?
  render () {
    // make sure to return some UI
    return (
      <h1>
        /*add the name of your favorite movie here!*/
      </h1>
    )
  }
}

export default Movie
```

Let's break down the things we see here...

#### `import React, { Component } from 'react'`

This imports React methods and the `Component` class from the React library.

#### `class Movie`

This is the component we're creating. In this example, we are creating a component and calling it "Movie."

#### `extends Component`

We inherit from the `Component` React library class to create our component definitions. Here, we are creating a new `Component` subclass called `Movie`.

- Because it extends (*inherits from*) `Component`, our `Movie` class gets to reuse code and capabilities from `React.Component`.

#### `render()`

Every component has a `render` method. The `render` method is what renders the component to the screen, so it controls what is displayed for this component. From this function, we return what we want to display.

- In our case, we are rendering a movie heading: `<h1>Movie!</h1>`.

> Note! That heading tag above looks like it's straight out of HTML, but it's actually a  language called JSX. For now, know that JSX will act like HTML when it's rendered to the screen.

#### `export default Movie`

This exposes the `Movie` class to other files.  This means that other files can `import` from the `App.js` file in order to use the `Movie` class.

Let's try that now. Open, up `App.js` and add the following to the `import`
statements at the top.

The `default` keyword means that if we try to import anything from this file that the app can't find, JavaScript will automatically revert to importing `Movie` instead.
Only one default export is allowed per file.

#### Import the New Component

Let's simplify our `App.js` to be just a function component.
```js
const App = () => (
  <div>
    <h1>Welcome to React!</h1>
  </div>
)
```

Then let's import the component we just built.

```js
import Movie from './Movie.js'
```

Then, we can render our movie component, like this:

```jsx
  const App = () => (
    <div>
      <h1>Welcome to React!</h1>
      <Movie />
    </div>
  )
```

#### Interpolation

Let's slightly modify the contents of our `src/Movie.js` file:

```js
// bring in React and Component from React
import React, {Component} from 'react';

// define our Movie component
class Movie extends Component {

  // what should the component render?
  render () {
  
    // make sure to return some UI
    const movie = {
      title: 'Lord of the React: Fellowship of React Components'
    }

    return (
      <h1>{movie.title}</h1>
    )
  }
}

export default Movie
```

Now, instead of hard coding the `return` value, we're interpolating using
`{movie.title}` (a variable local to the component).

So, JSX allows us to write code that strongly resembles HTML and can use
variable interpolation. It is eventually compiled to lightweight JavaScript
objects.

Your `Movie` component's `render` method:

- Currently returns JSX, not HTML.
- The JSX creates a DOM element with whatever you put in the `return ()` statement.
- Your component reads this and renders a movie heading (or multiple???).

### Code-along: React Developer Tools

The regular Chrome inspector can still be useful to us when working with React,
but it has some limitations. For one, it won't show us which components were
looking at. Also, once we start to use props and state in our applications,
we'll want a way to view those directly.

There's a Chrome extension called [React Dev Tools](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en)
that can help us achieve all that and more! Let's install it now, then use it
to inspect the simple app we've already created.

### Lab: JSX play time

Play around for 15 minutes adding different things to the `return` section of
the render method. Reference the [JSX documenation](https://reactjs.org/docs/jsx-in-depth.html) to find out what is and isn't
valid JSX!

### Team Lab:  Relaxr

The Relaxr team wants their website re-written in React so it is easier to manage and can eventually be connected to their API.  They've supplied us the [code for the original website](/relaxr).  Create componenents for the following parts of the page.  Be sure to organize the CSS as well.

- Header 
- Benefits section
- Testimonial section
- Aside 
- Footer
- Update the "Sign Up Now" and "Get it Now" buttons to both be "Sign Up Now" so you can use the same component

![relaxr](https://github.com/wdi-red-coral/hw-week_02-day_01-html-css/raw/solution/starter_code/images/relaxr_landing.jpg)
