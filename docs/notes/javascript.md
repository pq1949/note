
## JavaScript 指南 MDN

JavaScript 是一种基于原型而不是基于类的面向对象语言。正是由于这一根本的区别，其如何创建对象的层级结构以及对象的属性与属性值是如何继承的并不是那么清晰。

区别:
* 基于类的语言一个实例是一个类的实例化,实例的属性和其对应的类的属性完全一致，一旦定义了类，无法对类的属性进行更改。
* 基于原型的语言，原型对象可以作为一个模板，新对象可以从中获得原始的属性。任何对象都可以指定其自身的属性，既可以是创建时也可以在运行时创建。而且，任何对象都可以作为另一个对象的原型，从而允许后者共享前者的属性。

* https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide

## 详解Object.create(null)

* 你需要一个非常干净且高度可定制的对象当作数据字典的时候；
* 想节省hasOwnProperty带来的一丢丢性能损失并且可以偷懒少些一点代码的时候
用Object.create(null)吧！其他时候，请用{}。
for in 和 Object.create(null) 结合 就不用担心遍历到原型上的可枚举属性了

* https://juejin.im/post/5acd8ced6fb9a028d444ee4e

## for in 和 for of

* 对于纯对象的遍历，for..in要厉害一些
* for..of迭代更合适，因为还可以中断；如果需要知道索引，则forEach()更合适
* Object.keys()，Object.values()，Object.entries() 可以配合他们使用
* 注意:`for-of`循环不支持普通对象,但是如果你想迭代一个对象的属性,可以使用`for-in`循环(这也是它的本职工作)或者内建的`Object.keys()方法`

* https://www.zhangxinxu.com/wordpress/2018/08/for-in-es6-for-of/
* https://juejin.im/post/5aea83c86fb9a07aae15013b


## 闭包是函数和声明该函数的词法环境的组合
  闭包是由函数以及创建该函数的词法环境组合而成。这个环境包含了这个闭包创建时所能访问的所有局部变量
  * https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Closures
  * https://segmentfault.com/a/1190000011612140
  * https://juejin.im/entry/57d60f7067f3560057e37e25

## this、apply、call、bind
  * https://juejin.im/post/59bfe84351882531b730bac2

## You Don't Know JS
  * https://github.com/getify/You-Dont-Know-JS

## 位运算符在JS中的妙用
  * https://juejin.im/post/5a98ea2f6fb9a028bb186f34

## TypeScript
  * TypeScript 入门教程 https://ts.xcatliu.com/

## 动手写js沙箱
  * https://www.villainhr.com/page/2016/09/03/%E5%8A%A8%E6%89%8B%E5%86%99js%E6%B2%99%E7%AE%B1

## 33-js-concepts  ⭐️⭐️⭐️⭐️
33 concepts every JavaScript developer should know.

 https://github.com/leonardomso/33-js-concepts

## 30-seconds-of-code ⭐️⭐️⭐️⭐️
Curated collection of useful JavaScript snippets that you can understand in 30 seconds or less.

https://github.com/30-seconds/30-seconds-of-code?utm_source=gold_browser_extension


## JavaScript 标准参考教程⭐️⭐️

http://javascript.ruanyifeng.com/


## Javascript中的with关键字

http://luopq.com/2016/02/14/js-with-keyword/  (印象笔记有备份)


## Promise 串行
```js
function runPromiseByQueue(myPromises) {
  myPromises.reduce(
    (previousPromise, nextPromise) => previousPromise.then(() => nextPromise()),
    Promise.resolve()
  );
}

const createPromise = (time, id) => () =>
  new Promise(solve =>
    setTimeout(() => {
      console.log("promise", id);
      solve();
    }, time)
  );

runPromiseByQueue([
  createPromise(3000, 1),
  createPromise(2000, 2),
  createPromise(1000, 3)
]);
```

https://segmentfault.com/a/1190000016832285


## 手写Promise

https://segmentfault.com/a/1190000009809466


## 模块化介绍

[前端模块化：CommonJS,AMD,CMD,ES6](https://juejin.im/post/5aaa37c8f265da23945f365c)
[模块化七日谈 ](https://juejin.im/post/5aaa37c8f265da23945f365c)
[Common JS、AMD、CMD 和 UMD 的区别 ](https://github.com/G-Grant/Note/issues/3)

## mac中的文件允许输入斜线和反斜线

在做文件上传是需要考虑到mac的上传，禁止用户上传带有特殊字符的文件名

```js

const fileMatchName = (file) => {
  const regexp = new RegExp(/[\\\/:*?"<>|]+/)
  return !regexp.test(file.name)
}
```
