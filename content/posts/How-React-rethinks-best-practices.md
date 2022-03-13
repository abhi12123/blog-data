---
title: "How React Rethinks Best Practices"
date: 2021-11-21T19:08:50+05:30
---

[React.js](https://reactjs.org/) is currently the most popular front-end JavaScript library for building Web applications. It is an open-source JavaScript library that is used for building user interfaces. It renders the UI as per user requirements and plays nicely with any stack. In this article, we shall go through how React rethinks some of the best practices in web development.
## Separation of Concern
The [separation of concerns](https://en.wikipedia.org/wiki/Separation_of_concerns) (SoC) is one of the most fundamental principles in software development. The principle states that don’t write your program as one solid block, instead, break up the code into chunks that are finalized tiny pieces of the system each able to complete a simple distinct job.

Separation of concern aims to reduce coupling and to increase cohesion.

**Coupling** is the degree to which each module in a program relies on another. It is helpful as isolated problems are easy to deal with and the modules are highly likely to be unit testable. An increase in coupling means that the modules depend on each other and any change in one module might lead to cascading changes in others and it would be a nightmare to debug.

**Cohesion** is the degree to which elements of a module belong together. This is important as functionality wise the elements must make sense. Reduction in cohesion makes code harder to maintain. It won’t be easy to figure out where to make the change on need.
## Templates encourage a poor separation of concern
JavaScript templating refers to the client-side data binding method implemented with the JavaScript language. In templates, you will have display logic in one file and markup in another file. Display logic and markup are inevitably tightly coupled as well as highly cohesive. We can observe that templates, in fact, separate technologies, not concerns. above all that, **they are deliberately underpowered**.
* **Let’s take the case of Partial feature in [handlebars](https://handlebarsjs.com/):** Templates rely on primitive abstractions often. [“Partial”](https://handlebarsjs.com/guide/partials.html) is used for reusing templates. They are basically mini templates that can be included in other templates. The drawback of this approach is that reused child template gets all the variables the parent has in the current scope.
* **Flow control abstraction like [“Each”](https://handlebarsjs.com/guide/builtin-helpers.html#each)**: “Each” iterates through each item of a sequence and emits some markup in the traditional templating language. The downfall is that it is really hard to change the way it iterates through the list. **You don’t have the power of a programming language but the power of templating language which is deliberately underpowered**.
* **Inventing lots of new concepts that already exist in JavaScript**: Directives are classes that add additional behavior to elements in AngularJs. It creates a lot of concepts that were already there in JS. **The framework cannot know how to separate your concerns for you. it should only provide tools for the user to do it correctly. Rather than the language of the framework itself**.

## React — a highly cohesive and loosely coupled library
React uses components that mix markup and display logic. Markup and logic can be incorporated into individual components that match the app better unlike templating language. Moreover, the components display abstraction, composition, and expressivity.
* **Abstraction:** Components can be created using JavaScript function or class. They are unit testable and lintable.
* **Composition:** They are reusable.
* **Expressivity:** They use regular JavaScript expressions.

React ensures security from Cross-Site Scripting as it uses a library called React DOM, which is used to generate DOM. The library escapes the input automatically, so HTML is also escaped hence ensuring safety from XSS.

There is also an optional pre-processor that lets the user use HTML-like syntax for development called [JSX](https://reactjs.org/docs/introducing-jsx.html). It makes it easier for designers to contribute code.

React ensures that there is the ***accessibility of templates and the power of JavaScript***.
## The Virtual DOM
Building UI is hard because there are so many states to be managed over a web page. There are lots of UI elements, design iteration, user input, etc.

*Data changing over time is the root of all evil.*

We can no longer just refresh the page when the data changes. Currently, that is not a feasible solution and is also quite annoying from a user experience perspective.

React on the other hand re-renders the entire component on change. Components are [idempotent functions](https://www.bmc.com/blogs/idempotence/#:~:text=Idempotence%20is%20any%20function%20that,that%20classifies%20a%20function%27s%20behavior.) that describe your user interface at any point in time. React isolate data changes by using setState function in the case of Class components and user-defined functions in functional components. Now the question is it expensive?

React achieves this by using something called virtual DOM. Virtual DOM makes re-rendering fast. It is optimized for performance and memory footprint.

On every update, React build a new virtual DOM sub-tree and diff it with the old one. Then it computes the minimal set of DOM mutations and puts them in a queue and batch executes all updates.

It is fast because DOM is slow and react computes minimal DOM operations batched reads and writes for optimal DOM performance.

These are some of the ways in which React rethinks the best practices in web development. This article was based on [a talk by Pete Hunt](https://www.youtube.com/watch?v=x7cQ3mrcKaY&t=11s) from 2013. This was insightful as most of the tutorials on React deals with the How rather than the Why.