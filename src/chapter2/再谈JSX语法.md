# 编写注释
* 使用花括号包裹，花括号在jsx中代表其内部可以编写js代码
* 所以在js中怎样写注释，那么在jsx中的花括号中就怎么写注释

**多行注释**

```jsx
{/* 这里是一段普通的注释 */}
<div></div>
```

**单行注释**

```jsx
{
  // 这里是一段单行注释，注意花括号必须换行
}
<div></div>
```
# 添加class
原生html指定class时使用的是class属性，但是在jsx中，我们需要使用className来进行class的指定

这是因为jsx是存在于js文件中，而又因为class是js的关键字，为了避免冲突，所以jsx规定，DOM元素指定class应该采用className属性

# 展示html元素
```jsx
<li dangerouslySetInnerHTML={{__html: item}}></li>
```

# label标签的for属性
和class属性一样的原因，jsx中label标签上的for属性应该使用htmlFor