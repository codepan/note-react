react-redux是一个第三方模块，它可以让我们在React之中更加方便的使用Redux

**Provider 组件**

该组件是react-redux提供的一个核心API，这个组件可以向其所有的子组件提供store属性
```js
// src/index.js
import React from 'react'
import ReactDOM from 'react-dom'

import { Provider } from 'react-redux'
import store from './store'
import TodoList from './TodoList'

const App = (
  <Provider store={store}>
    <TodoList/>
  </Provider>
)
ReactDOM.render(App, document.getElementById('root'))
```