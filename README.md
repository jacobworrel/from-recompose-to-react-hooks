# from-recompose-to-react-hooks
A guide to help migrate from [recompose](https://github.com/acdlite/recompose) to the [React Hooks API](https://reactjs.org/docs/hooks-intro.html).

## State

##### Recompose
```javascript
import React from "react";
import { withState } from "recompose";

const Counter = ({ count, setCount }) => (
  <div>
    <div>{count}</div>
    <button onClick={event => setCount(count => count + 1)}>Increment</button>
    <button onClick={event => setCount(count => count - 1)}>Decrement</button>
  </div>
);

const enhance = withState('count', 'setCount', 0);

export default enhance(Counter);
```
[![Edit react-windowed-select](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/m44jwlzvrx)

##### React Hooks
```javascript
import React, { useState } from "react";

const Counter = () => {
  const [count, setCount] = useState(0);
  return (
    <div>
      <div>{count}</div>
      <button onClick={event => setCount(count => count + 1)}>Increment</button>
      <button onClick={event => setCount(count => count - 1)}>Decrement</button>
    </div>
  );
};

export default Counter;
```
[![Edit react-windowed-select](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/6471zjro33)

## Event Handlers

##### Recompose
```javascript
import React from 'react';
import { withHandlers } from 'recompose';

const Clicker = ({ id, handleClick }) => (
  <div onClick={handleClick}>Click me!</div>
);

const enhance = withHandlers({
  handleClick: (props) => (event) =>  {
    alert(`You just clicked ${props.id}`);
    event.stopPropagation();
  }
});

export default enhance(Clicker);
```
[![Edit react-windowed-select](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/nkzxrk9w9m)

##### React Hooks
```javascript
import React, { useCallback } from 'react';

const Clicker = ({ id }) => (
  <div onClick={useCallback(
    (event) => handleClick(event, id),
    [id]
  )}>
    Click me!
  </div>
);

function handleClick (event, id) {
  alert(`You just clicked ${id}`);
  event.stopPropagation();
}

export default Clicker;
```
[![Edit react-windowed-select](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/r4vx9oxmkq)