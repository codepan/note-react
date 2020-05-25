* 尽早的指定函数中的this
  ```js
  constructor () {
    this.handleChange = this.handleChange.bind(this)
  }
  ```
* 使用异步的setState
```js
handleChange (e) {
  const inputValue = e.target.value
  this.setState(() => ({
    inputValue
  }))
}
```
* 循环显示组件时指定组件的key值
```js
getTodoItems () {
  return this.state.list.map((item, index) => {
    return (
      <TodoItem
        key={index}
        content={item}
        index={index}
        remove={this.remove}
      />
    )
  })
}
```
* 合理使用shouldComponentUpdate
```js
shouldComponentUpdate (nextProps, nextState) {
  return nextProps.content !== this.props.content
}
```