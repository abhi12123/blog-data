---
title: "Why You Should Use Error Boundaries in React"
date: 2022-02-12T18:03:10+05:30
---

React Error Boundaries were introduced in React version 16 to generate a fallback UI in case a component were to crash. This was to ensure that a JavaScript error in a single component should not crash the whole app.  
Consider the following React application which renders the component `DisplayName` displaying the name according to the input data.

```jsx
import DisplayName from "./DisplayName";

function App() {
  return (
    <div className="App">
      <DisplayName name={{ firstName: "John", secondName: "Doe" }} />
      <DisplayName name={{ firstName: "Lex", secondName: "Luthor" }} />
      <DisplayName name={{ firstName: "Peter", secondName: "Parker" }} />
    </div>
  );
}

export default App;
```

The `DisplayName` component simply displays the name from the passed down `name` object.

```jsx
import React from "react";

export default function DisplayName({ name }) {
  return (
    <div
      style={{
        width: "600px",
        backgroundColor: "yellowgreen",
        margin: "auto",
        border: "black 1px solid",
      }}
    >
      {name.firstName} {name.secondName}
    </div>
  );
}
```

The browser will display something like this.

![code sample](https://miro.medium.com/max/723/1*iaKiQ9i-jsEewCeHqHMs8g.png)

If there were any errors while rendering any one of the components the entire application would be crashed and an empty page would be displayed on the production build. It would be hard to find and debug the error as well. For example, the following code will crash the application since the prop `name` is not being passed down to one of the components.

```jsx
import DisplayName from "./DisplayName";

function App() {
  return (
    <div className="App">
      <DisplayName />
      <DisplayName name={{ firstName: "Lex", secondName: "Luthor" }} />
      <DisplayName name={{ firstName: "Peter", secondName: "Parker" }} />
    </div>
  );
}

export default App;
```

## Implementing Error Boundaries

Error boundaries work as a JavaScript `catch {}` block, but for components. Error boundaries catch errors during rendering, in lifecycle methods, and in constructors of the whole tree below them. Error boundaries are, in fact class components, but will have two lifecycle methods `static getDerivedStateFromError` and/or `componentDidCatch()`. Error prone components can be passed down as their children.

`static getDerivedStateFromError()` can be used to render a fallback UI after an error has been thrown and `componentDidCatch()` can be used to log error information.

```jsx
import React, { Component } from "react";

export default class ErrorBoundary extends Component {
  constructor(props) {
    super(props);

    this.state = {
      hasError: false,
    };
  }
  static getDerivedStateFromError(error) {
    return { hasError: true };
  }
  componentDidCatch(error, info) {
    console.log(error, info);
  }
  render() {
    if (this.state.hasError) {
      return (
        <div
          style={{
            width: "600px",
            backgroundColor: "yellow",
            margin: "auto",
            border: "black 1px solid",
          }}
        >
          Fall Back UI
        </div>
      );
    }
    return this.props.children;
  }
}
```

How passing components as children of `ErrorBoundary` looks

```jsx
import DisplayName from "./DisplayName";
import ErrorBoundary from "./ErrorBoundary";

function App() {
  return (
    <div className="App">
      <ErrorBoundary>
        <DisplayName />
      </ErrorBoundary>
      <DisplayName name={{ firstName: "Lex", secondName: "Luthor" }} />
      <DisplayName name={{ firstName: "Peter", secondName: "Parker" }} />
    </div>
  );
}

export default App;
```

The browser will display output as

![code sample](https://miro.medium.com/max/754/1*XYsZV_AY7cXrE3eYJaH7tQ.png)

Instead of crashing the whole application.

You may wrap top-level route components to display a message to the user, just like how server-side frameworks often handle crashes or you may wrap individual components in an error boundary to protect them from crashing the rest of the application like above.

## Where Error Boundaries won’t work in React

- Event handlers
- Asynchronous code (e.g. `setTimeout` or `requestAnimationFrame` callbacks)
- Server side rendering
- Errors thrown in the error boundary itself (rather than its children)

## What about Event Handlers?

Error boundaries do not catch errors inside event handlers as React doesn’t need error boundaries to recover from errors in event handlers. Unlike the render method and lifecycle methods, the event handlers don’t happen during rendering. So if they throw, React still knows what to display on the screen.  
If you need to catch an error inside an event handler, use the regular JavaScript `try` / `catch` statement.
