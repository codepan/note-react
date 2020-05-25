Redux要求：
* store是唯一的
* 只有store能够改变自己的内容
* reducer可以接收state，但是绝不能修改state，且reducer是一个纯函数
  > 纯函数：给定固定的输入，就一定会有固定的输出，而且不会有任何副作用

Redux的核心API：
* createStore
* store.dispatch
* store.getState
* store.subscribe
