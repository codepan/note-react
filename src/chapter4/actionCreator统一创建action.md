之前的action我们在调用store.dispatch方法时，都是事先创建好，并且这些action全部都散落在组件的各个方法中

简单的项目按照上面的方式当然没有问题，但是如果编写的是大型的项目的话，Redux官方推荐使用actionCreator来统一管理创建各个action。这样做会有两个好处：
1. 统一管理action
2. 自动化测试容易

```js
// src/store/actionCreators.js
import * as actionTypes from './actionTypes'

export const getChangeInputValueAction = value => ({
  type: actionTypes.CHANGE_INPUT_VALUE,
  value
})

export const getAddTodoItemAction = value => ({
  type: actionTypes.ADD_TODO_ITEM,
  value
})

export const getRemoveTodoItemAction = value => ({
  type: actionTypes.REMOVE_TODO_ITEM,
  value
})
```

```js
// src/TodoList.js
import * as actionCreators from './store/actionCreators'
handleChange (e) {
  const action = actionCreators.getChangeInputValueAction(e.target.value)
  store.dispatch(action)
}

add () {
  const action = actionCreators.getAddTodoItemAction(this.state.inputValue)
  store.dispatch(action)
}

remove (index) {
  const action = actionCreators.getRemoveTodoItemAction(index)
  store.dispatch(action)
}
```