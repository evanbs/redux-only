# REDUX

[Live Example](https://codepen.io/vandoenterprise/pen/xxbRRRE?editors=0010)

## Documentation

### Redux Cycle

| Steps | Definition:    | Example:                     |
| ----- | -------------- | ---------------------------- |
| 1º    | Action Creator | Person dropping off the form |
| 2º    | Action         | The Form                     |
| 3º    | Dispatch       | Form Receiver                |
| 4º    | Reducers       | Departments                  |
| 5º    | State          | Compiled Department Data     |

### Redux Cycle

`Action Creator` produces an `Action`

`Action` gets fed to `Dispatch`

`Dispatch` forwards the action to `Reducers`

`Reducers` creates new `State`

`State` wait until we need to update state again

## Code Definition

### Action Creator

A function that returns JavaScript plain object with refer to `Action`

Example:

```javascript
const createPolicy = (name, amount) => {
    return {
        /* `Action` Block */
        type: 'CREATE_POLICY',
        payload: {
            name: name,
            amount: amount
        }
    };
};
```

### Action

Is like a form, have has the `Type` and the `payload`

Example:

```javascript
/* `Action Creator` Block */
    {
        type: 'CREATE_POLICY', // By convention the type is write using Uppercase
        payload: {
            name: name,
            amount: amount
        }
    }
/* `Action Creator` Block */
```

`Type` describe a purpose of the form
`Payload` provide some context on exactly the form is doing

### Dispatch

Is like a Form Receiver that receives the form or `Action` make a copy that form and send to all departments.

**\*Note**: dispatch is part of Redux library\*

```javascript
store.dispatch(createPolicy('Evandro', 20));
```

### Reducers

Are functions that model each department of the company. Each of these reducers will be called within an `Action` or `Action Creator`.

Is a function that receives two arguments
First argument is a slice of data that makes part of the "Department", second argument is the `Action`.

Example:

```javascript
/** First Argument: Define a default value for realy first time that code runs**/
const policies = (listOfPolicies = [], action) => {
    // Check if is a relevant action(form)
    if (action.type === 'CREATE_POLICY') {
        return [...listOfPolicies, action.payload.name];
    }

    // Is not relevante action
    return listOfPolicies;
};
```

**Note:** Always return a new _Array/String/Number etc. Never modified!_

### State

Represents the central data repository

```javascript
store.getState();
```

### Store

Is a assembly of different `Reducers` and `Action Creators` from Redux library.

Example:

```javascript
const { createStore, combineReducers } = Redux;

const ourDepartments = combineReducers({ policies, ...otherReducersGoesHere });

const store = createStore(ourDepartments);
```
