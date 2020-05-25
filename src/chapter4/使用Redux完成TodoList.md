```js
// src/TodoList.js
import React, { Component, Fragment } from 'react'
import TodoItem from './TodoItem'

import store from './store'

class TodoList extends Component {
  constructor (props) {
    super(props)

    this.state = store.getState()
    this.handleChange = this.handleChange.bind(this)
    this.add = this.add.bind(this)
    this.remove = this.remove.bind(this)

    // store.subscribe()方法用来订阅store中state的变化，一旦变化，就会触发向其传入的方法
    this.handleStoreChange = this.handleStoreChange.bind(this)
    store.subscribe(this.handleStoreChange)
  }

  handleChange (e) {
    const value = e.target.value
    const action = {
      type: 'changeInputValue',
      value
    }
    store.dispatch(action)
  }

  add () {
    const action = {
      type: 'addTodoItem',
      value: this.state.inputValue
    }

    store.dispatch(action)
  }

  remove (index) {
    const action = {
      type: 'removeTodoItem',
      value: index
    }
    store.dispatch(action)
  }

  handleStoreChange () {
    this.setState(store.getState)
  }
}

export default TodoList
```
```js
// src/store/reducer.js
const defaultState = {
  inputValue: '',
  list: []
}
export default (state = defaultState, action) => {
  const { type, value } = action
  // 这里实现对state的深拷贝，reducer规定state是只读的，不能直接修改
  let newState = JSON.parse(JSON.stringify(state))
  if (type === 'changeInputValue') {
    newState.inputValue = value
  }

  if (type === 'addTodoItem') {
    newState.inputValue = ''
    newState.list.push(value)
  }

  if (type === 'removeTodoItem') {
    newState.list.splice(value, 1)
  }

  return newState
}
```