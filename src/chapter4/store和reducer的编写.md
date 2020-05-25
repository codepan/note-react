src目录下创建一个store文件件，里面创建一个index.js文件

这个index.js文件就是编写store的地方
```js
// src/store/index.js
import { createStore } from 'redux'
import reducer from './reducer'

const store = createStore(reducer)

export default store
```

```js
// src/store/reducer.js
const defaultState = {
  inputValue: '123',
  list: ['haha', 'hehe']
}
export default (state = defaultState, action) => {
  return state
}
```
```js
// TodoList.js

// 引入store目录下的index.js文件
import store from './store'
class TodoList extends Component {
  constructor (props) {
    super(props)
    // store对象上有一个getState()方法，可以获取到刚才咱们定义的state
    this.state = store.getState()
  }
}
```