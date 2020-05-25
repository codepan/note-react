在没有redux-thunk中间件的时候，store.dispatch只能派发一个对象形式的action
```js
// store/actionCreators.js
export const getInitTodoListAction = value => ({
  type: actionTypes.INIT_TODO_LIST,
  value
})
```
```js
// TodoList.js
import store from './store'
import * as actionCreators from './store/actionCreators'

componentDidMount () {
  axios.get('/api/todolist').then(res => {
    // 这里的action就是一个对象形如: {type: 'xxx', value: 'xxx'}
    const action = actionCreators.getInitTodoListAction(res.data)
    store.dispatch(action)
  })
}
```

有了redux-thunk中间件，我们可以像下面这样，store.dispatch就可以接收一个函数作为action
```shell
# 安装 redux-thunk 中间件
yarn add redux-thunk
```
```js
// store/index.js
import { createStore, applyMiddleware } from 'redux'
import thunk from 'redux-thunk'
import reducer from './reducer'

const store = createStore(reducer, applyMiddleware(thunk))

export default store
```
```js
// store/actionCreators.js
export const getInitTodoListAction = value => ({
  type: actionTypes.INIT_TODO_LIST,
  value
})

export const findTodoList = () => {
  // 有了redux-thunk中间件，我们可以返回一个函数
  // 这个函数会在调用了store.dispatch之后被调用，并且Redux会向这个函数注入dispatch方法
  return dispatch => {
    axios.get('/api/todolist').then(res => {
      dispatch(getInitTodoListAction(res.data))
    })
  }
}
```
```js
import store from './store'
import * as actionCreators from './store/actionCreators'

componentDidMount () {
  // 这里的action是一个函数，可以将这个函数action直接传递给dispatch方法
  const action = actionCreators.findTodoList()
  store.dispatch(action)
}
```


如果我们使用了中间件，要继续使用redux-devtools时需要按照如下的方式进行使用
```js
// store/index.js
import { createStore, applyMiddleware, compose } from 'redux'
import thunk from 'redux-thunk'
import reducer from './reducer'

const composeEnhancers = window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__ ? window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__({}) : compose

const enhancer = composeEnhancers(applyMiddleware(thunk))

const store = createStore(reducer, enhancer)

export default store
```

我们可能会有这样的疑问：上一节我们在生命周期函数中发送异步请求获取数据写的好好的，这里为什么要使用中间件来完成这件事情，代码量不但没有减少，反而增多了。这是因为目前咱们的项目比较小，
随着项目的膨胀，异步请求写在生命周期函数中会变得越来越复杂，越来越不好维护
