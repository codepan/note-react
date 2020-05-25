自己实现React，我们刚开始的思路可能是这样的：

**方案1：传统方式**

1. state数据
2. JSX模板
3. 数据+模板 结合，生成真是的DOM，并显示
4. state发生改变
5. 数据+模板 结合，生成真是的DOM。替换原始的DOM

缺陷：
* 第一次生成一个完整的DOM片段
* 第二次生成一个完整的DOM片段
* 第二次的DOM会替换掉第一次的DOM，非常消耗性能

**方案2：文档碎片**

换种思路，我们按如下的方式去做，性能上就可以得到一些提升：
1. state数据
2. JSX模板
3. 数据+模板 结合，生成真是的DOM，并显示
4. state发生改变
5. 数据+模板 结合，生成真是的DOM，但是并不会替换原生的DOM
6. 拿新的DOM（DocumentFragment）和原始的DOM做比对，找出差异
7. 例如之前的例子中inputValue发生了变化，只用新的DOM中的input元素，替换掉老的DOM中的input元素即可，其它的DOM都不需要改动

新的方案虽然提高了DOM替换的性能，但是它有带来了新的性能损耗，那就是新老DOM做比对的时间。这样一来，一处提高了性能，另一处有损耗了性能，最终性能上的提升仍然是微乎其微的。

缺陷：
* 性能的提升并不明显

**方案3：虚拟DOM**

1. state数据
2. JSX模板
3. 生成虚拟DOM（虚拟DOM就是一个JS对象， 用它来描述真实的DOM）【生成虚拟DOM会损耗一点性能，但是它的损耗极小】
  ```js
  // 虚拟DOM
  const virtualDOM = ['div', {id: 'box'}, ['span', {}, 'Hello World']]
  ```
4. 使用虚拟DOM生成真实的DOM，并显示
  ```html
  <!-- 真实DOM -->
  <div id="box"><span>Hello World</span></div>
  ```
5. state发生变化
6. 数据+模板 生成新的虚拟DOM【极大的提升了性能因为js生成js对象的速度，远比js生成DOM的速度快得多】
  ```js
  // 虚拟DOM
  const virtualDOM = ['div', {id: 'box'}, ['span', {}, 'codepan']]
  ```
7. 比较新老虚拟DOM的区别（找到区别是span中的内容）【比较的是js对象，比两个DOM进行比较的速度快得多】
8. 直接操作DOM，改变span中的内容，生成新的DOM
  ```html
  <!-- 真实DOM -->
  <div id="box"><span>codepan</span></div>
  ```

优点：
* 减少了真实DOM的创建，取而代之的是创建虚拟DOM
* 减少了真实DOM的比对，取而代之的是虚拟DOM的比对

