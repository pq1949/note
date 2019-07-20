### 常用 module 包

- `xss`
- `lodash`
- `moment`
- `dayjs`
- `push.js`
- `linkifyjs`
- `b64-to-blob`
- `script.js`
- `i18next`
- `chimee-player`
- `chalk`
- `ora`
- `rimraf`
- `feather-icons`  simply beautiful open source icons

### 规范 guide
1. [Alloyteam代码规范](https://github.com/AlloyTeam/CodeGuide)
2. [JavaScript规范](https://github.com/adamlu/javascript-style-guide)
3. [如何写出漂亮的 JavaScript 代码](https://juejin.im/post/5d0e11196fb9a07eee5ed6d2?utm_source=gold_browser_extension)
4. [O2前端规范文档](https://github.com/o2team/guide)
5. [JavaScript规范](https://github.com/adamlu/javascript-style-guide)
## JSTips ⭐️⭐️⭐️

http://www.jstips.co/

## JavaScript 指南 MDN

JavaScript 是一种基于原型而不是基于类的面向对象语言。正是由于这一根本的区别，其如何创建对象的层级结构以及对象的属性与属性值是如何继承的并不是那么清晰。

区别:

- 基于类的语言一个实例是一个类的实例化,实例的属性和其对应的类的属性完全一致，一旦定义了类，无法对类的属性进行更改。
- 基于原型的语言，原型对象可以作为一个模板，新对象可以从中获得原始的属性。任何对象都可以指定其自身的属性，既可以是创建时也可以在运行时创建。而且，任何对象都可以作为另一个对象的原型，从而允许后者共享前者的属性。

- https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide

## 详解 Object.create(null)

- 你需要一个非常干净且高度可定制的对象当作数据字典的时候；
- 想节省 hasOwnProperty 带来的一丢丢性能损失并且可以偷懒少些一点代码的时候
  用 Object.create(null)吧！其他时候，请用{}。
  for in 和 Object.create(null) 结合 就不用担心遍历到原型上的可枚举属性了

- https://juejin.im/post/5acd8ced6fb9a028d444ee4e

## for in 和 for of

- 对于纯对象的遍历，for..in 要厉害一些
- for..of 迭代更合适，因为还可以中断；如果需要知道索引，则 forEach()更合适
- Object.keys()，Object.values()，Object.entries() 可以配合他们使用
- 注意:`for-of`循环不支持普通对象,但是如果你想迭代一个对象的属性,可以使用`for-in`循环(这也是它的本职工作)或者内建的`Object.keys()方法`

- https://www.zhangxinxu.com/wordpress/2018/08/for-in-es6-for-of/
- https://juejin.im/post/5aea83c86fb9a07aae15013b

## 闭包是函数和声明该函数的词法环境的组合

闭包是由函数以及创建该函数的词法环境组合而成。这个环境包含了这个闭包创建时所能访问的所有局部变量

- https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Closures
- https://segmentfault.com/a/1190000011612140
- https://juejin.im/entry/57d60f7067f3560057e37e25

## this、apply、call、bind

- https://juejin.im/post/59bfe84351882531b730bac2

## You Don't Know JS

- https://github.com/getify/You-Dont-Know-JS

## 位运算符在 JS 中的妙用

- https://juejin.im/post/5a98ea2f6fb9a028bb186f34

```js
// 所有非数值转换成0
// 所有大于等于 0 等数取整数部分
this.length >>> 0
// https://www.zhihu.com/question/20693429
// https://github.com/seajs/seajs/issues/150
```

## TypeScript

- TypeScript 入门教程 https://ts.xcatliu.com/

## 动手写 js 沙箱

- https://www.villainhr.com/page/2016/09/03/%E5%8A%A8%E6%89%8B%E5%86%99js%E6%B2%99%E7%AE%B1

## 33-js-concepts ⭐️⭐️⭐️⭐️

33 concepts every JavaScript developer should know.

https://github.com/leonardomso/33-js-concepts

## 30-seconds-of-code ⭐️⭐️⭐️⭐️

Curated collection of useful JavaScript snippets that you can understand in 30 seconds or less.

https://github.com/30-seconds/30-seconds-of-code?utm_source=gold_browser_extension

## JavaScript 标准参考教程 ⭐️⭐️

http://javascript.ruanyifeng.com/

## Javascript 中的 with 关键字

http://luopq.com/2016/02/14/js-with-keyword/ (印象笔记有备份)

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

## 手写 Promise

https://segmentfault.com/a/1190000009809466

## 模块化介绍

[前端模块化：CommonJS,AMD,CMD,ES6](https://juejin.im/post/5aaa37c8f265da23945f365c)
[模块化七日谈 ](https://juejin.im/post/5aaa37c8f265da23945f365c)
[Common JS、AMD、CMD 和 UMD 的区别 ](https://github.com/G-Grant/Note/issues/3)

## mac 中的文件允许输入斜线和反斜线

在做文件上传是需要考虑到 mac 的上传，禁止用户上传带有特殊字符的文件名

```js
const fileMatchName = file => {
  const regexp = new RegExp(/[\\\/:*?"<>|]+/);
  return !regexp.test(file.name);
};
```

## 稀疏数组

创建稀疏数组的方式

```js
const a = [, , ,]; // [empty × 3]

const b = new Array(3); //[empty × 3]

const bb = new Array();
bb.length = 3; // [empty × 3]

const c = [];
c[100] = 100; // [empty × 100, 100]

const c = [];
c.length = 10; // [empty × 10]

const d = [0, 1, 2];
delete d[1]; // [0, empty, 2]
```

通过 `for in` `map` `forEach` 等方式遍历稀疏数组不能按照数组的长度遍历完整的数组，会直接跳过那些是 `empty` 的位置

创建密集数组

```js
const a = Array.apply(null, Array(3)); // [undefined, undefined, undefined]
arr.map((elem, index) => index); // [0, 1, 2, 3]

const b = Array(3).fill() // https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/fill
```

http://www.jstips.co/en/javascript/3-array-hacks/

### Object.is

```js
NaN === NaN is false, but Object.is(NaN, NaN) is true
+0 === -0 is true, but Object.is(+0, -0) is false
-0 === +0 is true, but Object.is(-0, +0) is false
```

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/is

### 如何衡量一个人的 JavaScript 水平？

https://www.zhihu.com/question/22855484/answer/657320514

### 输入框

1. `input.selectionStart` `input.selectionEnd` 可以用来设置 input 中被选中的文字
2. `autoComplete` 关闭自动提示

### 多行文字显示省略号

```js
export function truncateStr(str, len) {
  if (!str) return str;
  let targetStrLen = 0;
  let strLen = str.length;
  let targetStr = "";
  for (let i = 0; i < strLen; i++) {
    let a = str.charAt(i);
    //中文字符的长度经编码之后大于4，算两个字符
    targetStrLen += escape(a).length > 4 ? 2 : 1;
    targetStr = targetStr.concat(a);
    if (targetStrLen >= len) {
      targetStr = targetStr.concat("...");
      return targetStr;
    }
  }
  //如果给定字符串小于指定长度，则返回源字符串；
  if (targetStrLen < len) {
    return str;
  }
}
```

### 转义

```js
export const escape2Html = (str) => {
  if (!str) return str

  let arrEntities = {
    'lt': '<',
    'gt': '>',
    'nbsp': ' ',
    'amp': '&',
    'quot': '"',
    'apos': '\'',
    '#39': '\''
  }
  return str.replace(/&(lt|gt|nbsp|amp|quot|apos|#39);/ig, function (all, t) {
    return arrEntities[t]
  })
}
```

### js 字符串自动补全

[JS字符串补全方法padStart()和padEnd()简介](https://www.zhangxinxu.com/wordpress/2018/07/js-padstart-padend/)
```js
var timestamp = +String(timestamp).padEnd(13, '0')

var month = String(new Date().getMonth() + 1).padStart(2, '0')
```

### 优雅处理错误信息

```js
try {
    Func();
} catch (e) {
    location.href = "https://stackoverflow.com/search?q=[js]+" + e.message;
}

//
const wrapWithTryCatch = fn => (...args) => {
  try {
    return fn.apply(null, args)
  } catch (e) {
    console.log(e)
    window.open("https://stackoverflow.com/search?q=[js]+" + e.message)
  }
}
```
### 优雅处理Async/Await参数

```js
function AsyncTo(promise) {
    return promise.then(data => [null, data]).catch(err => [err]);
}
const [err, res] = await AsyncTo(Func());

```
[灵活运用JavaScript开发技巧](https://juejin.im/post/5cc7afdde51d456e671c7e48#heading-8)


###  支持中文和url-safe编码的Base64
```js
function urlSafeBase64(base64) {
  return base64
    .replace(/=/g, "")
    .replace(/\+/g, "-")
    .replace(/\//g, "_");
}
```
或者使用这个库
https://github.com/brianloveswords/base64url


### Why is my webpack build slow?
https://samsaccone.com/posts/why-is-my-webpack-build-slow.html


### 节流 防抖
`core-decorators/lib/throttle`
```js
throttle(fn, wait, {
  leading,
  trailing
})
// leading 默认为 true , 设置成 false 时 第一次不执行
// trailing 默认为 true , 奢侈成 false 时 最后一次不执行

// 两个都设置成 false 时 都不执行
```

`core-decorators/lib/debounce`

```js
debounce(fn, wait,immediate)

// immediate 默认为 false ，只有当间隔大于 wait 时才开始执行
// immediate 设置成 true 时 会先立即执行一次
```

### canvas 转 blob
```js
import b64toBlob from 'b64-to-blob'
export function upgradeFileName (oldName, suffix = '.jpg') {
  if (oldName) {
    return oldName.replace(/\.\w+$/, suffix)
  } else {
    return Date.now() + suffix
  }
}
/**
 * canvas to blob
 * @param {*} canvas - the canvas
 * @param {*} callback - callback when blob is generated
 * @param {*} oldName - old file name
 * @param {*} mime - blob file type
 */
export function canvasToBlob (canvas, callback, oldName, mime) {
  if (canvas.msToBlob) {
    const blob = canvas.msToBlob()               // IE下同步是调用
    blob.name = upgradeFileName(oldName, '.png') // IE下默认是png
    console.log(111, blob.name)
    callback(blob)
  } else if (canvas.toBlob) {
    canvas.toBlob(blob => {
      blob.name = upgradeFileName(oldName, '.jpg')
      callback(blob)
    }, mime)
  } else {
    const dataUrl = canvas.toDataURL(mime, 1.0).split(',')[1]
    const blob = b64toBlob(dataUrl, mime)
    blob.name = upgradeFileName(oldName, '.jpg')
    callback(blob)
  }
}
```

### Content Security Policy   CSP

[Content-Security-Policy的实战应用](https://www.jianshu.com/p/a8b769e7d4bd)
[Content Security Policy 入门教程](http://www.ruanyifeng.com/blog/2016/09/csp.html)


### Web Worker
[怎么在 ES6+Webpack 下使用 Web Worker](https://juejin.im/post/5acf348151882579ef4f5a77)
[Web Workers w3c](https://w3c.github.io/workers/)
[Web Worker 网道](https://wangdoc.com/javascript/bom/webworker.html)
[Canvas 最佳实践（性能篇）](http://taobaofed.org/blog/2016/02/22/canvas-performance/)
