### [react-lifecycle-methods-diagram](https://github.com/wojtekmaj/react-lifecycle-methods-diagram)
  * http://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/


### react 动画库
  * [react-motion](https://github.com/chenglou/react-motion) ⭐️⭐️⭐️⭐️⭐️
    * [react-motion-drawer](https://github.com/stoeffel/react-motion-drawer)
  * [react-spring](https://github.com/react-spring/react-spring)⭐️⭐️⭐️⭐️⭐️

### 数据流
  * [MobX](https://suprise.gitbooks.io/mobx-cn/content/fp.html)
  * [Mobx使用详解](https://www.jianshu.com/p/505d9d9fe36a)


### redux 源码
  * [Redux入坑进阶-源码解析](https://github.com/ecmadao/Coding-Guide/blob/master/Notes/React/Redux/Redux%E5%85%A5%E5%9D%91%E8%BF%9B%E9%98%B6-%E6%BA%90%E7%A0%81%E8%A7%A3%E6%9E%90.md)    [备份](../backup/redux)

    中间中的`next`参数是下一个中间件，最后一个中间件的`next`是`store.dispatch`

    `middlewares=[a,b,c,d,e]` => `applyMiddleware(...middlewares)` => `compose(...middlewares.map(middleware => middleware({getState,dispatch})))(store.dispatch)`
    => `compose(...chain)` => `a(b(c(d(e(store.dispatch)))))`

    ![redux](../imgs/redux.png)

### Hooks, React Render props, HOC,  Mixins

 * [[译] 使用 Render props 吧！](https://juejin.im/post/5a3087746fb9a0450c4963a5)
 * [Render Props 官网](https://reactjs.org/docs/render-props.html)
 * [React v16.7 "Hooks" - What to Expect](https://zhuanlan.zhihu.com/p/47684983)


#### A Complete Guide to useEffect ⭐️⭐️⭐️

https://overreacted.io/a-complete-guide-to-useeffect/
https://overreacted.io/zh-hans/a-complete-guide-to-useeffect/


###  深入React fiber 链表和DFS
https://mp.weixin.qq.com/s/Tp05MoV1bQi7rgpYnz1Xhg


### React ref 的前世今生

使用ref时最好使用函数的形式进行负责，字符串的情况有时会出错，并且也影响性能

遇到一个使用string的ref错误，在这里报错, 改成了函数形式就可以了

![](../imgs/ref-error1.png)

![](../imgs/ref-error.png)



https://juejin.im/post/5b59287af265da0f601317e3
https://stackoverflow.com/questions/37468913/why-ref-string-is-legacy
https://stackoverflow.com/questions/28519287/what-does-only-a-reactowner-can-have-refs-mean



### ant-design 动态更改From.Item校验规则


Validate 后 Form 会缓存结果，如果你直接动态改 rule 的话，加一个 force 来强制无视缓存就好了

https://codesandbox.io/s/oj9r74k329


https://github.com/ant-design/ant-design/issues/13689
