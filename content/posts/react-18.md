---
title: "Behold, React 18 !"
date: 2022-04-09T11:24:44+05:30
---

A new version of React was released on the 29th of March this year. The latest version, React 18, includes some out-of-the-box improvements, including concurrent rending, new APIs, and much more. In this article, we shall go through some of the new features that have been introduced in React v18.

## What is Concurrent React?
Many of the new features in React v18.0 are on top of a concept called Concurrent Renderer. This enables us to use concurrent React, which helps us to prepare multiple versions of a UI at the same time. Right now, the concurrent React is optional, which means it is only enabled when you use a concurrent feature.  

Previous versions of React used a single, uninterrupted, synchronous transaction. That is, with synchronous rendering, once an update starts rendering, nothing can interrupt it until the user can see the result on the screen.

In a concurrent render, this is not always the case. React may start rendering an update, pause in the middle, then continue later, or It may even abandon an in-progress render altogether. React guarantees that the UI will appear consistent even if a render is interrupted.  

React can prepare new screens in the background without blocking the main thread. This means the UI can respond immediately to user input even if it’s in the middle of a large rendering task, creating a fluid user experience.

Almost all the updates in the new version are based on the new concurrent rendering mechanism.

## New Features in React

### Automatic Batching
Most often you might have faced a situation where multiple state updates had to be performed. Batching is when React groups multiple state updates into a single re-render for better performance. 

```js
// Before: only React events were batched.
setTimeout(() => {
  setCount(c => c + 1);
  setFlag(f => !f);
  // React will render twice, once for each state update (no batching)
}, 1000);

```

React till now had only executed Batching inside React event handlers, whereas updates inside promises, setTimeout, native event handlers or any other event were not batched by default. With automatic batching, these updates will be batched automatically.

```js
// After: updates inside of timeouts, promises,
// native event handlers or any other event are batched.
setTimeout(() => {
  setCount(c => c + 1);
  setFlag(f => !f);
  // React will only re-render once at the end (that's batching!)
}, 1000);
```


### Transitions
A transition is a new concept in React. Updates are divided into two types in React. Urgent updates and Transition updates
**Urgent updates** are those updates that reflect direct interaction, like typing, clicking, pressing, and so on. These updates need immediate response to match our intuitions about how physical objects behave. Otherwise, they might feel a bit odd. 
**Transition updates** are those updates that transition the UI from one view to another. Transitions are different because the user doesn’t expect to see every intermediate value on the screen.

For example, when you interact with a filter feature, you expect the filter button itself to respond immediately when you click. However, the actual results may transition separately. A small delay might occur and is often expected. And if you change the filter again before the results are done rendering, you only expect the latest result.

React has introduced `startTransition` API which can be used inside an input event to inform React which updates are urgent and which are transitions.  

Updates inside a `startTransition` are handled as non-urgent and will be interrupted if more urgent updates like clicks or keypresses come in. If a transition gets interrupted by the user (for example, by typing multiple characters in a row), React will throw out the stale rendering work that wasn’t finished and render only the latest update. 

```js
import {startTransition} from 'react';

// Urgent: Show what was typed
setInputValue(input);

// Mark any state updates inside as transitions
startTransition(() => {
  // Transition: Show the results
  setSearchQuery(input);
});
```

### New Suspense Features
Suspense lets you declaratively specify the loading state for a part of the component tree if it’s not yet ready to be displayed.

```jsx
<Suspense fallback={<Spinner />}>
  <Comments />
</Suspense>
```

This lets us build higher-level features on top of it. In React 18, the support for Suspense on the server has been added and expanded its capabilities using concurrent rendering features.

### New Client and Server Rendering APIs
React introduced some new APIs to implement concurrent react. It has to be used instead of default APIs or else new features in React 18 would not work

#### React DOM Client - new APIs
* `createRoot`: New method to create a root to render or unmount. Use it instead of `ReactDOM.render`.
* `hydrateRoot`: New method to hydrate a server-rendered application. Use it instead of `ReactDOM.hydrate`.

Both `createRoot` and `hydrateRoot` accept a new option called `onRecoverableError`. This notifies when React recovers from errors during rendering. By default, React will use `reportError`, or `console.error` in the older browsers.

#### React DOM Server - new APIs
* `renderToPipeableStream`: for streaming in Node environments.
* `renderToReadableStream`: for modern edge runtime environments, like Deno and Cloudflare workers.
The existing `renderToString` method keeps working but is discouraged.

### New Hooks

* `useId` - a new hook for generating unique IDs on both the client and server
* `useTransition` - `useTransition` and `startTransition` let you mark some state updates as not urgent. Other state updates are considered urgent by default. React will allow urgent state updates (for example, updating a text input) to interrupt non-urgent state updates (for example, rendering a list of search results).
* `useDeferredValue` -  lets you defer re-rendering a non-urgent part of the tree. It is similar to debouncing, but there is no fixed time delay, so React will attempt the deferred render right after the first render is reflected on the screen. The deferred render is interruptible and doesn’t block user input
* `useSyncExternalStore` -  allows external stores to support concurrent reads by forcing updates to the store to be synchronous. It removes the need for `useEffect` when implementing subscriptions to external data sources.
* `useInsertionEffect` -  CSS-in-JS libraries to address performance issues of injecting styles in render. This hook will run after the DOM is mutated, but before layout effects read the new layout.  

In short, the new updates have been largely focused on optimization, removing unwanted renders, leading to increased performance.
