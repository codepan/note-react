上一节中我们的action散落在各自的方法中，并且action.type都是一个字符串，并且TodoList组件中和reducer文件中的action.type必须保持一致，一旦字符串拼写错误，就会导致代码报错

所以Redux官方推荐我们将action的type统一管理，使用一个叫做actionTypes.js的文件对所有的action.type进行常量导出，然后分别在组件中和reducer文件中引入action.type常量即可

```js
// src/store/actionTypes.js
export const CHANGE_INPUT_VALUE = 'changInputValue'
export const ADD_TODO_ITEM = 'addTodoItem'
export const REMOVE_TODO_ITEM = 'removeTodoItem'
```

```js
// src/TodoList.js
import * as actionTypes from './store/actionTypes'
handleChange (e) {
  const value = e.target.value
  const action = {
    type: actionTypes.CHANGE_INPUT_VALUE,
    value
  }
  store.dispatch(action)
}

add () {
  const action = {
    type: actionTypes.ADD_TODO_ITEM,
    value: this.state.inputValue
  }

  store.dispatch(action)
}

remove (index) {
  const action = {
    type: actionTypes.REMOVE_TODO_ITEM,
    value: index
  }
  store.dispatch(action)
}
```

```js
// src/store/reducer.js
import * as actionTypes from './actionTypes'
// state的默认值
const defaultState = {
  inputValue: '',
  list: []
}
export default (state = defaultState, action) => {
  const { type, value } = action
  // 这里实现对state的深拷贝，reducer规定state是只读的，不能直接修改
  let newState = JSON.parse(JSON.stringify(state))
  if (type === actionTypes.CHANGE_INPUT_VALUE) {
    newState.inputValue = value
  }

  if (type === actionTypes.ADD_TODO_ITEM) {
    newState.inputValue = ''
    newState.list.push(value)
  }

  if (type === actionTypes.REMOVE_TODO_ITEM) {
    newState.list.splice(value, 1)
  }
  return newState
}
```