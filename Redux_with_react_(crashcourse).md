# REACT + REDUX
## TERMS
### Store & State (A Single Source of Truth)
The state is the data, and the store is where it’s kept.
redux gives you a store, and lets you keep state in it, and get state out, and respond when the state changes. But that’s all it does.
react-redux lets you connect pieces of the state to React components.

### Reducer (A Pure Function)
It takes the current **state**, and an **action**, and returns the **newState**.
- Reducer Rule #1: Never return undefined from a reducer.
- Reducer Rule #2: Reducers must be pure functions.

### Actions object and Dispatch method (A Payload and a Launchpad)
TLDR; Any connected component can **dispatch** **actions** as the payload. Store calls the **Reducer**. Reducer returns a **NewState**.
- An Action is plain object with a property called *type*. eg. ```{ type: 'ACTION_NAME' }```. \
- In order to make an action DO something, you need to dispatch it using ```store.dispatch({Action})```. \
- Redux calls ```reducer(state, action)```, reducer ```return (NewState)```.
- Redux Store State replaced by the NewState.
  - ```reducer(state = {Default State Object}, action) => return {A new State object}```

### Provider and Connect (The Wiring)
To make every component be able to access the Redux Store on demand, entire app is wrapped with the **Provider** component. \
But not automatically. We’ll need to use the **connect** function on our components to access the store.

## IMPLEMENTATION
A simple button component which changes its text when clicked

```javascript
/** APP INDEX.JS **/
import { Provider } from "react-redux";
import { createStore } from "redux";

/** REDUCER: takes the current state, and an action, and returns the newState **/
function reducer(state = { buttonText: "Not Clicked Yet" }, action) {
  return action.type === "BUTTON_CLICK" ? { buttonText: "Clicked" } : state;
}
// APP & STORE CREATION
const store = createStore(reducer);
const App = () => (
  <provider store="{store}">
    <mycomponent/>
  </provider>
);

/** COMPONENT **/
import React from "react";
import { connect } from "react-redux";

// ACTION object
const action = {
  type: "BUTTON_CLICK"
}

// Action DISPATCHER
const MyComponent = (props) => (
  <button onclick="{props.dispatch(action)}">
    props.buttonText
  </button>
)

// MAP STATE TO PROPS: inject the redux state variables as props to the component
const mapStateToProps = (state) => { buttonText: state.buttonText }

// CONNECT component to the Redux Store
export default connect(mapStateToProps)(MyComponent);
```
