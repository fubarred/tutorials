# REACT + REDUX
## TERMS
### Store & State
The state is the data, and the store is where it’s kept.
redux gives you a store, and lets you keep state in it, and get state out, and respond when the state changes. But that’s all it does.
react-redux lets you connect pieces of the state to React components.

### Reducer
It takes the current state, and an action, and returns the newState
Reducer Rule #1: Never return undefined from a reducer.
Reducer Rule #2: Reducers must be pure functions.

### Actions and Dispatch
An Action is plain object with a property called *type*. eg. ```{ type: 'ACTION_NAME' }```
In order to make an action DO something, you need to dispatch it.
The store object has a built-in function called dispatch. Call it with an action, and Redux will call your reducer with that action (and then replace the state with whatever your reducer returned).
```store.dispatch({ type: "INCREMENT" });```

### Provider and Connect
By wrapping the entire app with the *Provider* component, every component in the app tree will be able to access the Redux store if it wants to.
But not automatically. We’ll need to use the *connect* function on our components to access the store.

## IMPLEMENTATION
A simple button component which changes its text when clicked

```javascript
/** APP INDEX.JS **/
import { Provider } from "react-redux";
import { createStore } from "redux";

// takes the current state, and an action, and returns the newState
function reducer(state = { buttonText: "Not Clicked Yet" }, action) {
  return action.type === "BUTTON_CLICK" ? { buttonText: "Clicked" } : state;
}
const store = createStore(reducer);
const App = () => (
  <provider store="{store}">
    <mycomponent/>
  </provider>
);

/** COMPONENT **/
import React from "react";
import { connect } from "react-redux";

const action = {
  type: "BUTTON_CLICK"
}

const MyComponent = (props) => (
  <button onclick="{props.dispatch(action)}">
    props.buttonText
  </button>
)

// inject the redux state variables as props to the component
const mapStateToProps = (state) => { buttonText: state.buttonText }

export default connect(mapStateToProps)(MyComponent);
```
