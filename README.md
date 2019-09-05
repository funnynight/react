# PubNub React SDK v2.0

Welcome to the new PubNub React SDK!

## System requirements

To use the React SDK, you need:

* React 16.8 or above
* Javascript xyz
* **[what else?]**

## PubNubProvider

The PubNubProvider makes available a PubNub client instance to a React component tree. You instantiate the provider as follows (note that your publish and subscribe keys are contained in the `pubnub.json` file):

```js
import PubNub from 'pubnub';
import { PubNubProvider } from '../../src/index';

const pubNubConfig = require('../config/pubnub.json');
const pubNubClient = new PubNub(pubNubConfig.Demo.keySet);

const App = () => {
  return (
    <PubNubProvider client={pubNubClient}>
      <MyRootComponent />
    </PubNubProvider>
  );
};

export default App;
```

### PubNubProvider props

The PubNubProvider component takes a single prop:

* **client** is the required pubNubClient instance. This is used by all components that require PubNub functionality.

## PubNubConsumer

The PubNubConsumer allows you to access the client instance you made available with a PubNubProvider.

### PubNubConsumer props

The PubNubConsumer component takes a single prop:

* **client** is the required pubNubClient instance. This is used by all components that require PubNub functionality.

### Example PubNubConsumer usage

Once you've created a PubNubProvider, you can access the client with a PubNubConsumer.

```js
import React from 'react';
import PubNub from 'pubnub';
import { PubNubProvider } from '../PubNubProvider';
import { PubNubConsumer } from '../PubNubConsumer';
import { getPubNubContext } from '../PubNubContext';

const pubNubConfig = require('../config/pubnub.json');
const pubNubClient = new PubNub(pubNubConfig.Demo.keySet);

const App = () => {
  <PubNubProvider client={pubNubClient}>
    <PubNubConsumer>
      {client => "success!" /* do something now */ }
    </PubNubConsumer>
  </PubNubProvider>
};

```

## Context

<!-- lifted from reactjs.org -->
Context provides a way to pass data through the component tree without having to pass props down manually at every level.

Context is designed to share data that can be considered “global” for a tree of React components, such as the current authenticated user, theme, or preferred language.

In a typical React application, data is passed top-down (parent to child) via props, but this can be cumbersome for certain types of props (e.g. locale preference, UI theme) that are required by many components within an application. Context provides a way to share values like these between components without having to explicitly pass a prop through every level of the tree.

### Context.Provider

<!-- lifted from reactjs.org -->
Every Context object comes with a Provider React component that allows consuming components to subscribe to context changes.

Accepts a `value` prop to be passed to consuming components that are descendants of this Provider. One Provider can be connected to many consumers. Providers can be nested to override values deeper within the tree.

All consumers that are descendants of a Provider will re-render whenever the Provider’s `value` prop changes. The propagation from Provider to its descendant consumers is not subject to the `shouldComponentUpdate` method, so the consumer is updated even when an ancestor component bails out of the update.

Changes are determined by comparing the new and old values using the same algorithm as `Object.is`.

### Class.contextType

<!-- lifted from reactjs.org -->
The `contextType` property on a class can be assigned a Context object created by `React.createContext()`. This lets you consume the nearest current value of that Context type using `this.context`. You can reference this in any of the lifecycle methods including the render function.

### Context.Consumer

<!-- lifted from reactjs.org -->
A React component that subscribes to context changes. This lets you subscribe to a context within a function component.

### Example context usage

```js
// do the thing
```

## The usePubNub hook

Hooks are a new feature added in React 16.8 that allow you to use React features without writing a class. For a general overview of hooks, refer to [the React documentation](https://reactjs.org/docs/hooks-intro.html).

The PubNub hook lets you interact with PubNub in function components:

```js
import React, { useState, useEffects } from 'react';
import { usePubNub } from '../../src/index';
import { getPubNubContext } from '../context/PubNubContext';

function Example() {

  usePubNub(() => {
    // do the things

  });

  return (
    <div>
      <p>You did the thing</p>
    </div>
  );
}
```

> **Note**: As you might expect, the `usePubNub` hook requires cleanup. For more information on the cleanup concept, refer to [the React documentation](https://reactjs.org/docs/hooks-effect.html#effects-with-cleanup).

### Example usage
