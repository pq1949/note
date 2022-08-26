## @babel/preset-env

https://babeljs.io/docs/en/babel-preset-env

默认只会导入大于 stage3 的垫片，可以通过 shippedProposals: true 配置导入 stage3的垫片

### useBuiltIns

 "usage" | "entry" | false, defaults to false.

1. entry  根据代码中入口位置的import和  browserslistrc 配置 自动导入需要的包

in
```js
import "core-js";
```
out
```js
import "core-js/modules/es.string.pad-start";
import "core-js/modules/es.string.pad-end";
```

in
```js
import "core-js/es/array";
import "core-js/proposals/math-extensions";
```

out
```js
import "core-js/modules/es.array.unscopables.flat";
import "core-js/modules/es.array.unscopables.flat-map";
import "core-js/modules/esnext.math.clamp";
import "core-js/modules/esnext.math.deg-per-rad";
import "core-js/modules/esnext.math.degrees";
import "core-js/modules/esnext.math.fscale";
import "core-js/modules/esnext.math.rad-per-deg";
import "core-js/modules/esnext.math.radians";
import "core-js/modules/esnext.math.scale";
```

2. usage ,项目的入口不需要主动import，会自动根据代码中的实际使用情况和 browserslistrc 按需导入， 通常项目打包中不会处理 node_modules的第三方包，如果依赖的第三方包没做好es6转译，可能会有bug

in
```js
var a = new Promise();
```

out
```js
import "core-js/modules/es.promise";
var a = new Promise();
```

3. false， 在项目入口中 `import "core-js"` 后把整个包导入，不会自动按指定的环境去导入，代码体积会大一些


### corejs

当 useBuiltIns 是 entry 或者 usage 时 需要指定一个 corejs 版本 ，否则会出一个警告

```
WARNING (@babel/preset-env): We noticed you're using the `useBuiltIns` option without declaring a core-js version. Currently, we assume version 2.x when no version is passed. Since this default version will likely change in future versions of Babel, we recommend explicitly setting the core-js version you are using via the `corejs` option.

You should also be sure that the version you pass to the `corejs` option matches the version specified in your `package.json`'s `dependencies` section. If it doesn't, you need to run one of the following commands:

  npm install --save core-js@2    npm install --save core-js@3
  yarn add core-js@2              yarn add core-js@3

More info about useBuiltIns: https://babeljs.io/docs/en/babel-preset-env#usebuiltins
More info about core-js: https://babeljs.io/docs/en/babel-preset-env#corejs
```

同时指定 corejs 版本时 最好指定次版本号， 因为 3 会被 当做 3.0 处理，这样最新的一些语法垫片可能就无法打进去了

默认情况下 只会导入稳定的es特性
 1. 使用 `useBuiltIns: "entry"` 时  手动导入需要的还处于 proposal  的垫片，例如

 ```js
 import "core-js/proposals/string-replace-all"
 ```
2.  当使用 `useBuiltIns: "usage"` 时
   1 设置 shippedProposals 为 true 会导入 stage3 的特性
   2. `{ version: "3.8", proposals: true }` 会导入 corejs 3.8 版本的所有 proposal




## @babel/plugin-transform-runtime

https://babeljs.io/docs/en/babel-plugin-transform-runtime

此包做了三件事情

a. 使用 async functions 时， 自动引入 regenerator  (通过 regenerator 开关控制， 默认 true)
b. 不污染全局的方式引入垫片 (通过 corejs 控制 默认 false)
c. 自动把内联的帮助方法转换成引入 @babel/runtime/helpers 中的包，减少打包体积 （通过 helpers 开关控制， 默认 true)



1. corejs

false, 2, 3 or { version: 2 | 3, proposals: boolean }, defaults to false.

建议项目开发中 此配置为 false，让 preset-env 去处理垫片，如果是库模式的开发，为了使得引入的垫片不污染使用方的全局环境，这里最好设置一个版本号，建议使用 3 ，（2只能对全局变量生成垫片，对于实例上的方法无法导入垫片，比如 [].includes）


同 preset-env  默认不导入 proposal 的垫片，可以设置 `proposals: true` 选项导入 proposal 垫片

不同的版本依赖的安装包不同

false	  -->   npm install --save @babel/runtime
2       --> 	npm install --save @babel/runtime-corejs2
3	      -->   npm install --save @babel/runtime-corejs3


2.  helpers
boolean, defaults to true.

是否把 babel 内联的辅助代码片段统一从 `@babel/runtime/helpers` 引入

in
```js
class Person {}
```

without helper
```js
"use strict";

function _classCallCheck(instance, Constructor) {
  if (!(instance instanceof Constructor)) {
    throw new TypeError("Cannot call a class as a function");
  }
}

var Person = function Person() {
  _classCallCheck(this, Person);
};
```

with helper
```js
"use strict";

var _classCallCheck2 = require("@babel/runtime/helpers/classCallCheck");

var _classCallCheck3 = _interopRequireDefault(_classCallCheck2);

function _interopRequireDefault(obj) {
  return obj && obj.__esModule ? obj : { default: obj };
}

var Person = function Person() {
  (0, _classCallCheck3.default)(this, Person);
};
```

3. regenerator

boolean, defaults to true

只有 preset-env 时, 如果用到 async 会把 _regeneratorRuntime 的实现打包到代码中

```
"presets": [
    [
      "@babel/preset-env",
      {
        "useBuiltIns": "usage",
        "corejs": "3.23"
      }
    ]
  ]
```


有preset-env 同时有 plugin-transform-runtime 时，会变成引入 @babel/runtime 中的 regenerator, 此时

plugin-transform-runtime 的 regenerator 设置为false时 会在引入一个会污染全局的 regenerator

```js
require("regenerator-runtime/runtime.js");
```

plugin-transform-runtime 的regenerator  设置为 true 时 则会从 runtime-corejs3引入不污染全局的regenerator包

```js
var _regenerator = _interopRequireDefault(require("@babel/runtime-corejs3/regenerator"));
```
