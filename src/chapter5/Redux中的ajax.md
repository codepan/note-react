```js
// store/actionTypes.js
export const INIT_TODO_LIST = 'initTodoList'
```

```js
// store/actionCreators.js
export const getInitTodoListAction = value => ({
  type: actionTypes.INIT_TODO_LIST,
  value
})
```

```js
// store/reducer.js
import * as actionTypes from './actionTypes'
// state的默认值
const defaultState = {
  inputValue: '',
  list: []
}
export default (state = defaultState, action) => {
  const { type, value } = action
  let newState = JSON.parse(JSON.stringify(state))
  if (type === actionTypes.INIT_TODO_LIST) {
    newState.list = value
  }
  return newState
}
```

```js
// TodoList.js
import store from './store'
import * as actionCreators from './store/actionCreators'
import axios from 'axios'
componentDidMount () {
  axios.get('/api/todolist').then(res => {
    const action = actionCreators.getInitTodoListAction(res.data)
    store.dispatch(action)
  })
}
```