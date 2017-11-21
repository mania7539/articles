---
published: true
tags:
  - react-js
  - javascript
  - redux
  - web
---


* Setup modules for the react js and redux project before you run your npm server

```bash
$ npm i -S react react-redux redux react-dom redux-thunk 
```

## Write React Js in Redux Concept

* You can create a new empty file with the batch command

```
$ echo.> [filename: index.js]
```

* /src/action/

```js
/* index.js */

import constants from "../constant";

export default {

    // This is an action creator to create a todo list item object
    createTodoItem(todo) {
        return {
            type: constants.CREATE_TODO_ITEM,
            data: todo
        }
    }

}
```


* /src/component/container/

```js
/* Todo.js */

import React, { Component } from 'react';
import { connect } from "react-redux";

class Todo extends Component {
    constructor() {
        super();
        this.state = {
            nextTodo: { name: '', description: '' },
            // todoList: []
        }
    }

    makeTheFirstLetterUppercase(string) {
        return string.charAt(0).toUpperCase() + string.slice(1);
    }

    updateTodo(field, event) {
        // console.log("UPDATE TODO: " + field + " == " + event.target.value);
        let nextTodo = Object.assign({}, this.state.nextTodo);
        nextTodo[field] = this.makeTheFirstLetterUppercase(event.target.value);
        this.setState({
            nextTodo: nextTodo
        });

    }

    addTodo(event) {
        // console.log("ADD TODO: " + JSON.stringify(this.state.nextTodo)); // use JSON.stringify to make the json into formatted string

        // let todoList = Object.assign([], this.state.todoList);
        // todoList.push(this.state.nextTodo);
        // this.setState({
        //     todoList: todoList,
        //     nextTodo: { name: '', description: '' } // use this line to clear the text which was typed in the input fields
        // });

    }

    render() {
        // grab the todo from the reducer 'todo' and get property 'todos'
        const todoList = this.props.todo.todos;
        return (
            <div className="container-fluid">
                <div className="row justify-content-center">
                    <div className="col-4">
                        <h2>Todo List</h2>
                        <ol>
                            {
                                todoList.map((item, i) => {
                                    return <li key={i}>{item.name}</li>
                                })
                            }
                        </ol>

                        <input value={this.state.nextTodo.name} onChange={this.updateTodo.bind(this, "name")} className="form-control" type="text" placeholder="Name" /><br />
                        <input value={this.state.nextTodo.description} onChange={this.updateTodo.bind(this, "description")} className="form-control" type="text" placeholder="Description" /><br />
                        <button onClick={this.addTodo.bind(this)}>Add Todo</button>
                    </div>
                </div>

            </div>

        );
    }
}

// connection component to store with redux
const stateToProps = (state) => {
    return {
        // maps your custom state to props, so you need to query the reducer definition in your store
        todo: state.todo
    }
};

const dispatchToProps = (dispatch) => {
    return {

    }
}

export default connect(stateToProps, dispatchToProps)(Todo);


```


* src/constant/

```js
/* index.js */

```


* src/reducer/

```js
/* index.js */

import todoReducer from "./todoReducer";

export {
    todoReducer
}

```


```js
/* todoReducer.js */

import constants from '../constant';

var initialState = {
    todos: [
        { name: 'Groceries', description: 'pick up groceries' },
        { name: 'Laundry', description: 'drop off laundry at dry cleaner' },
        { name: 'Fantasy team', description: 'update fantasy teams' },
    ]
};

export default (state = initialState, action) => {
    switch (action.type) {
        case (constants.CREATE_TODO_ITEM):
            console.log("CREATE_TODO_ITEM");
            return state;
        
        default: 
            return state;

    }
};

```


* src/store/

```js
/* index.js */

import { createStore, applyMiddleware, combineReducers } from "redux";
import thunk from "redux-thunk";
import { todoReducer } from "../reducer";

let stores = null;

export default {
    createStore() {
        // combine all reducers, one by one here, and give them a specific name:
        const reducers = combineReducers({
            todo: todoReducer
        });

        // create the store, which can be access outside the scope
        stores = createStore(
            reducers,
            applyMiddleware(thunk)
        );

        return stores;
    },

    getCurrentStore() {
        return stores;
    }
}

```


* src/

```js
/* App.js */

import React, { Component } from 'react';
import './App.css';
import Todo from './component/container/Todo';
import { Provider } from "react-redux";
import store from "./store";

class App extends Component {
  render() {
    return (
      <Provider store={store.createStore()} className="fluid-container">
        <Todo />
      </Provider>
    );
  }
}

export default App;

```
