通过上一节的讲解，这里要澄清一点就是：

JSX 并不是页面中的真实DOM，它就是一个模板，React会将其余state和props结合，结合之后生成虚拟DOM，有了虚拟DOM之后，再生成真实的DOM

React中将JSX是按照下面的方式一步步将其变成真实的DOM的：

> JSX ---> createElement ---> JS对象（虚拟DOM) ---> 真实的DOM

对上面的内容做一个详细说明

首先我们使用JSX编写了一个模板
```jsx
<div>item</div>
```
接着React底层会将上面的JSX使用React.createElement()方法变成JS对象
```js
/*
方法接收三个参数：
* 第一个参数是标签名
* 第二个参数是属性键值对
* 第三个参数是标签的内容
*/
React.createElement('div', {}, 'item')
```

可以看出，即使我们不使用JSX，而是直接使用createElement方法一样可以完成工作，但是createElement比较底层，编写起来不是那么的容易，

所以React发明人脑洞大开，发明出了JSX这个东西，JSX（`Javascript XML`的简称）


virtualDOM的优点：
* 性能提升了
* 它使得跨端应用得以实现，例如React Native，可以和Android或IOS一样开发原生应用
  * 原生应用比web应用体验好这是毋庸置疑的，但是React中有virtualDOM性能很高，所以照样与其媲美
  * 真实DOM浏览器认识，但原生应用是无法识别的。好在原生应用可以认识虚拟DOM即JS对象
  * 有了虚拟DOM，如果此时处于浏览器环境，那么React可以将其转换为真实DOM渲染；如果此时处于原生应用环境，那么React又可以将其转换成原生的组件
  * 所以说React既能开发网页应用，又能开发原生应用