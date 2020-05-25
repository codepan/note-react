redux中间件，指的是谁和谁的中间呢？答案是：action和store之间

在之前，action只能是一个对象，通过store.dispatch方法将action派发给store

现在当我们使用了redux-thunk之后，action就可以是一个函数

中间件就是对dispatch的方法的一个封装。调用store.dispatch将action派发给store之后，中间件会在它俩中间做一层拦截，
判断action是对象还是函数，如果是对象，则和原先的流程一致；如果是函数，则中间件会调用这个函数，让其执行，执行之后就会获取到一个对象形式的action

到此，中间件其实就是对redux的dispatch方法的一个升级或者说封装，封装之后dispatch这个方法既可以接受一个对象，又可以接受一个函数，就是这么简单。

Redux的中间件有很多，我们目前使用redux-thunk就是Redux中间件其中之一

* redux-thunk
* redux-logger
* redux-saga