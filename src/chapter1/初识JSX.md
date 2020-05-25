JSX 其实就是可以让开发者在js文件中像在html文件中那样 自由的书写html语法


书写时需要注意一下两点：
* 不能将JSX写成字符串，即不能加单引号或者双引号
* 自定义的React 组件，在使用时也是通过标签的形式使用，但是自定义组件的标签首字母必须大写

```js
import React from 'react';
function App () {
  /* 错误写法
  return (
    '<div>hello world</div>'
  )
  */

  /* 错误写法
  return '<div>hello world</div>'
  */

  return (
    <div>hello world</div>
  )
}
export default App
```

```js
import React from 'react'
import ReactDOM from 'react-dom'
/* 错误写法
import app from './App'
ReactDOM.render(<app />, document.getElementById('root'))
*/
import App from './App'
ReactDOM.render(<App />, document.getElementById('root'))
```
