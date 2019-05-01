# from-recompose-to-react-hooks

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