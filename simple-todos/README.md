<img src="https://d14xs1qewsqjcd.cloudfront.net/assets/og-image-logo.png" width="300">

# INTRO TO METEOR/BLAZE

| LEARNING OBJECTIVES |
|---|
| Introduction to Meteor/Blaze |
| Installing Meteor |
| Minimongo |
| Subscriptions and Publications |
| Hot Code Push |
| Todo App Walkthrough |

## Introduction to Meteor/Blaze

"Meteor is a full-stack JavaScript platform for developing modern web and mobile applications. Meteor includes a key set of technologies for building connected-client reactive applications, a build tool, and a curated set of packages from the Node.js and general JavaScript community." - (http://docs.meteor.com/#/full/)

Blaze is the default frontend framework that comes with Meteor. It is a Meteor-only package, and may be replaced with AngularJS or ReactJS.

- Meteor (or MeteorJS) is a JavaScript framework that is great for Rapid Application Development (RAD).

- It is built on top of Node.js (meaning that meteor uses node features such as package.json, node_modules, npm install, etc. 	

- Created by Meteor Development Group and initially released in 2012.

- It was designed to be easy to learn and use. One of Meteor's principles is "simplicity equals productivity".

- Why Meteor? (https://www.quora.com/Should-I-use-Meteor-Why)

## Installing Meteor

- Current version of Meteor: 1.4 (https://www.meteor.com/install)

	- OSX/Linux users can install from terminal:
	<br>
	`curl https://install.meteor.com/ | sh`

	- Windows users should click on link above for install button


## Minimongo

- Although real-world React apps require developer tools to compile and build the app, the React docs show us a way to do the necessary processing right in the browser.

- Setting up the playground requires:
	1. Loading several scripts into our _index.html_
	2. Loading our code into script tags and setting the type like this:<br>`<script type="text/babel" src="js/app.js"></script>`<br>- OR -<br>You can also play with code inline between script tags like this:<br>`<script type="text/babel">`<br>`  // your code in here`<br>`</script>`

- Let's create a `react-tutorial` directory and an _index.html_ inside of it.

<!--- <span style="text-decoration:line-through">`cd` into `react-tutorial` and copy/paste the setup code from the [Getting Started](https://facebook.github.io/react/docs/tutorial.html#getting-started) section into _index.html_.</span>
-->
- Go to [this page](https://facebook.github.io/react/downloads/single-file-example.html), view the source (View -> Developer -> View Source), copy the HTML and paste it into your _index.html_.

- We are going to put our code in a file and include it like this `<script type="text/babel" src="js/app.js">` - this way we will have syntax highlighting. **Create** the `js` directory and **touch** an `app.js` file inside of it.

- Our page will need to be served up by a server, so spin up your favorite server (I'll use `http-server`).

- Lastly, we will be using a special syntax known as JSX to describe the views in our components.  Let's make Atom aware of this syntax by installing the `react` package.

## Hot Code Push

Here is the [link to the new tutorial](https://facebook.github.io/react/tutorial/tutorial.html). Your favorite, another Tic-Tac-Toe game! Follow along with me and we'll work through the tutorial together.

You can do the tutorial directly in CodePen if you want, but I suggest that you copy the starter code from each file into your own files. This will allow you to use the Chrome dev tools later.

<!--#### The tutorial below has been replaced!

- Let's get a taste of writing some React by going through some of the steps of React's excellent online tutorial.

- Along the way, we'll get some practice converting ES5 `React.createClass` code into ES2015 classes.

- We'll follow the tutorial until we get to step `// tutorial6.js` (_Adding Markdown_).

- Let's skip `// tutorial6.js` & `// tutorial7.js`.

- Continue the tutorial by completing `// tutorial8.js` through `// tutorial10.js`.

- Finally, time permitting, let's end the tutorial by completing `// tutorial15.js` through `// tutorial19.js` where we see how to work with forms to add a new comment.  However, there are a couple of caveats here due to the fact we have defined our components as ES2015 classes:
	- The `getInitialState` method you will see applies only to components created with `createClass`. Components defined as classes set their initial state in a `constructor` method.
	- `createClass` automatically binds methods to the instance of the component (this). However, with classes, we will have to use the `bind` method to accomplish the same thing and I will show you two different ways of using it. I can also show you how to use an arrow function in certain cases.-->

## Todo App Walkthrough

#### Everything is JavaScript

- Unlike other frameworks like AngularJS, Ember, etc., React does not use HTML to define any part of the UI.

- When coding a React app, we only use JavaScript.

- If everything is JavaScript, how do we define a component's HTML? Glad you asked...

#### JSX

- The React library has a `React.createElement` method used to create DOM elements.

- However, there's a more readable, more elegant and more fun way to code the UI than using pure JS - JSX.

- JSX (JavaScript XML) looks like HTML, complete with attributes.  Let's see how a component might render a `<div>` styled using Bootstrap's _jumbotron_ class:

	```js
	... components have a render method - other code omitted
	  render() {
	    return <div className="jumbotron">Best Application EVER</div>;
	  }
	```
	Note that JSX uses `className` instead of `class`.  This is necessary because `class` is a keyword in JavaScript.  Instead, JSX uses the same JS property names found on DOM elements.

- JSX must be compiled into pure JavaScript before our browser can understand it.  This pre-processing is one of the reasons why developing React apps require tools that need to be installed and configured...

#### Tooling

- Real-world React apps require "building".

- A build process must be run on the developers workstation for the purpose of:

	- Compiling JSX into native JavaScript
	- Transforming and processing other assets as necessary
	- Loading of JavaScript modules
	- Packaging JS files and dependencies into a single JS `bundle.js` file

- There are several build tools available.  However, the one that has gained the most traction of late for developing React apps is _Webpack_.

- Regardless of the tooling, configuring them for best results is not trivial.

- Luckily, the React team has released, `create-react-app`, a CLI that:
	- Generates a minimal React app
	- Sets up the dev environment for:
		- Live compiling & page refresh
		- Testing
		- Building for production

#### Components

- User interfaces in React are composed of components.

- Each component is defined by a single JS `class`.  For example, a component used to render a _comment_ in an app might be defined with a class named **Comment**:

	```js
	class Comment extends React.Component {
	  render() {
	    return (
	      <div>Comment: {this.props.comment}</div>
	    );
	  }
	}
	```

- Prior to ES2015, components were being defined in ES5 using the `React.createClass` method.

- Components can only return a single, outer DOM element.  However, that single DOM element may have child DOM elements nested within it.

- Most React apps will have a single main root component rendered inside of an element on the _index.html_ page. The React app would be rendered with the ReactDOM library like this:

	```js
	ReactDOM.render(
	  <App />,
	  document.getElementById('react-app')
	);
	```

	This assumes that you have an element in your body like:

	```html
	<body>
		<main id="react-app"></main>
	</body>
	```

	and a main component, named `App`, that might be something like this:

	```js
	class App extends React.Component {
	  render() {
	    return (
	      <div>
	        <MenuBar />
	        <GameBoard />
	        <Footer />
	      </div>
	    );
	  }
	}
	```

- It is a better practice to have numerous small components

- Components will often render child components.  For example:
