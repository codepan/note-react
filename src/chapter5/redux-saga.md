```js
// store/actionTypes.js
export const INIT_TODO_LIST = 'initTodoList'
export const FIND_TODO_LIST = 'findTodoList'
```

```js
// store/actionCreators.js
export const getInitTodoListAction = value => ({
  type: actionTypes.INIT_TODO_LIST,
  value
})

export const getFindTodoListAction = () => ({
  type: actionTypes.FIND_TODO_LIST
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
  // 这里实现对state的深拷贝，reducer规定state是只读的，不能直接修改
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

componentDidMount () {
  const action = actionCreators.getFindTodoListAction()
  store.dispatch(action)
}
```

```js
// store/sagas.js
import { takeEvery, put } from 'redux-saga/effects'
import { FIND_TODO_LIST } from './actionTypes'
import { getInitTodoListAction } from './actionCreators'
import axios from 'axios'

function* findTodoList () {
  const res = yield axios.get('/api/todolist')
  const action = getInitTodoListAction(res.data)
  yield put(action)
}

function* sagas () {
  yield takeEvery(FIND_TODO_LIST, findTodoList)
}
export default sagas
```

```js
// store/index.js
import { createStore, applyMiddleware } from 'redux'
import createSagaMiddleware from 'redux-saga'

import reducer from './reducer'
import sagas from './sagas'

const sagaMiddleware = createSagaMiddleware()
const store = createStore(reducer, applyMiddleware(sagaMiddleware))

sagaMiddleware.run(sagas)

export default store
```