---
title: "React Explained and Made Simple"
date: 2021-11-21T17:16:42+05:30
---


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1635659888350/RiQ52UEMy.png)

# Is React a Framework ?
As per the landing page of React , it is a JavaScript library to build user interfaces. Its not a framework, but a library.
Angular, Vue, Next.js, Gatsby, Redwood.js etc are examples for frameworks. A framework includes resources that a large-scale application might need : creating forms, running automated tests, making network requests etc.
Whereas React itself does not include many of these functionalities. Core react is used only to build User Interfaces. In order to build complete React applications, you will need to choose the required packages and tools on your own. For example, for forms and validation React Hook Form or Formik can be used and for testing React Testing Library or Jest can be used.

# Features of React
## Component Based
In React, a web page can be divided to encapsulated blocks of code called components. These components can be composed to create complex UIs. Component logic is written in JavaScript instead of templates in React. Required data can be passed to the web app via these components easily, which renders accordingly on change.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1635659993376/DjJ1PAZvy.png)

## Declarative
Simple views can be designed for each state in your application and data can be passed into it. React will efficiently update and render just the right components when your data changes.
## Learn Once, Write Anywhere
React can be used along with multiple technology stacks. Thus you can develop new features in React without rewriting existing code. React can also render on the server using Node and it can power mobile apps using React Native.

# Add React to a Website
React can be added in small parts to your website and then can be gradually expand its presence
## Step 1 : Add a DOM Container to the HTML
Open the HTML page you want to edit and Add an empty ```<div>``` tag to mark the spot where you want to display something with React.
A unique id HTML attribute is given to div which will allow us to find it from the JavaScript code later and display a React component inside of it. You can place a “container” ```<div>``` like this anywhere inside the ```<body>``` tag. You may have as many independent DOM containers on one page as you need. They are usually empty — React will replace any existing content inside DOM containers.

```html
<!--… existing HTML … --> 
<div id='name-container'></div>
<!-- … existing HTML … -->
```
## Step 2 : Add the Script Tags
You will have to add three ```<script>``` tags to the HTML page right before the closing </body> tag. The first two tags load React. The third one will load your component code.
```html
<!-- … other HTML … -->
<script src="https://unpkg.com/react@17/umd/react.development.js" crossorigin></script>
<script src="https://unpkg.com/react-dom@17/umd/react-dom.development.js" crossorigin></script>
<!-- Load our React component. -->
<script src="name_component.js"></script>
```
## Step 3: Create a React Component
Create a file called ```name_container.js```. This code defines a React component called ```NameContainer```.
```js
'use strict';
const e = React.createElement;

class NameContainer extends React.Component {
  render() {
    return e('div',null,'Joe');
  }
}
const domContainer = document.querySelector('#name-container');
ReactDOM.render(e(NameContainer), domContainer);
```
**React** is used to create components. Create Element function of React takes Three arguments

- Type : div, h1, p, span etc
- [props] : class, id, onClck etc
- […children] : string, another DOM element

**ReactDOM** is used to render components in DOM. Render function of ReactDOM takes two arguments
- Element to Render
- Dom Container into which it should be rendered

## Step 4: Try React with JSX ( optional )
In the previous example we only relied on features that are natively supported by browsers. This is why we used a JavaScript function call to tell React what to display: However, React also offers an option to use JSX instead. While JSX is completely optional, many people find it helpful for writing UI code. Add this `<script>` tag to your page and you can use JSX in any `<script>` tag by adding `type='text/babel'`

```html
<script src=”https://unpkg.com/babel-standalone@6/babel.min.js"></script>
<script src=”name_component.js” type=”text/babel”></script>
```

```name_container.js``` can be modified accordingly
```jsx
"use strict";
const e = React.createElement;
class NameContainer extends React.Component {
  render() {
    return <div>Joe</div>
  }
}
const domContainer = document.querySelector("#name-container");
ReactDOM.render(e(NameContainer), domContainer);
```
# Recommended Toolchains
The React team primarily recommends these solutions:
- Create React App : If you’re learning React or creating a new single-page app
- Next.js : If you’re building a server-rendered website with Node.js
- Gatsby : If you’re building a static content-oriented website
- Others : Neutrino, Nx, Parcel, Razzle

Create React App is a comfortable environment for learning React. It is the best way to start building a new single-page application in React. You can use the latest JavaScript features and it provides a nice developer experience and optimizes your app for production.
You’ll need to have Node >= 14.0.0 and npm >= 5.6 on your machine
To create a project, run:
```console
npx create-react-app my-app
cd my-app
npm start
```
Create React App doesn’t handle backend logic or databases. it just creates a frontend build pipeline which you can use it with any backend you want. Under the hood, it uses Babel and webpack, but you don’t need to know anything about them. When you’re ready to deploy to production, running npm run build will create an optimized build of your app.
