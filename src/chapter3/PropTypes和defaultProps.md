```js
import React, { Component } from 'react'
// 设置prop类型的工具类，这个包安装react包时会自动安装
import PropTypes from 'prop-types'

class TodoItem extends Component {
  constructor (props) {
    super(props)
    console.dir(PropTypes)
    this.handleClick = this.handleClick.bind(this)
  }

  render () {
    const { content } = this.props
    return (
      <div onClick={this.handleClick}>
        {content}
      </div>
    )
  }

  handleClick () {
    const { remove, index } = this.props
    remove(index)
  }

  // 指定组件可能接收的prop
  static propTypes = {
    content: PropTypes.string.isRequired,
    remove: PropTypes.func,
    index: PropTypes.number
  }
  // 指定各个prop的默认值
  static defaultProps = {
    content: 'todo1' // content prop的默认值为todo1
  }
}

export default TodoItem
```