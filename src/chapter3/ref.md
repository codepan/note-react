使用ref可以获取到DOM，然后对DOM进行操作

```js
handleChange (e) {
  // 在React中，我们可以使用e.target来获取DOM节点
  console.dir(e.target)
  const inputValue = e.target.value
  this.setState(() => ({
    inputValue
  }))
}
```

```js
<input
  className='input'
  value={this.state.inputValue}
  onChange={this.handleChange}
  {/* 也可以使用ref属性来获取DOM节点 */}
  ref={input => {this.input = input}}
/>
```

在React16.*的版本中，ref为一个函数，React在调用这个函数时会自动注入一个参数，这个参数即为DOM节点的引用，我们拿到这个参数之后可以将其挂载到this对象中，然后再React组件实例中就可以使用this.input的方式来操作DOM了

但是实际上，React是及其不推荐使用ref来操作DOM的，React官方推荐我们使用**数据驱动**的形式来编写代码，除非万不得已，否则我们永远不应该主动去操作DOM，而是只需要操作数据，然后让React帮助我们去实现DOM的变化

为什么不推荐操作DOM，因为操作DOM可能会带来一些问题，下面通过一个例子来看这个问题

```jsx
<div>
  <input
    className='input'
    value={this.state.inputValue}
    onChange={this.handleChange}
    ref={input => {this.input = input}}
  />
  <button onClick={this.add}>提交</button>
</div>
<ul ref={ul => {this.ul = ul}}>
  {this.getTodoItems()}
</ul>
```

```js
add () {
  this.setState(prevState => ({
    list: [...prevState.list, prevState.inputValue],
    inputValue: ''
  }))

  const lis = this.ul.querySelectorAll('li')
  console.log(lis.length)
}
```

点击提交按钮，我们在add方法中获取ul下面的所有的li组成的数组的长度，按理说第一次点击按钮的时候，控制台输出1才对，但是发现输出的却是0。

这是因为setState它是一个异步函数，当你操作DOM输出li的数量这句代码会在setState里面的函数执行之前被执行，解决这个问题，setState提供了第二个参数，参数也是一个函数，它可以理解为setState完成DOM的重新渲染之后的回调。

```js
add () {
  this.setState(prevState => ({
    list: [...prevState.list, prevState.inputValue],
    inputValue: ''
  }), () => {
    const lis = this.ul.querySelectorAll('li')
    console.log(lis.length)
  })
}
```
