### typescript 学习资料
https://github.com/typescript-cheatsheets/react-typescript-cheatsheet
https://basarat.gitbooks.io/typescript/content/docs/getting-started.html

Practical Advanced TypeScript https://egghead.io/courses/practical-advanced-typescript

Use Types Effectively in TypeScript https://egghead.io/courses/use-types-effectively-in-typescript


What are the best resources for learning TypeScript? Asking for a friend. @resource
https://twitter.com/mjackson/status/1128500194000220166


awesome-typescript
https://github.com/semlinker/awesome-typescript

[如何编写 Typescript 声明文件](https://blog.jiasm.org/2018/10/12/%E5%A6%82%E4%BD%95%E7%BC%96%E5%86%99-Typescript-%E5%A3%B0%E6%98%8E%E6%96%87%E4%BB%B6/)

[TypeScript - 一种思维方式](https://juejin.im/post/5cd6387d518825682348442d)

[react-redux-typescript-guide](https://github.com/piotrwitek/react-redux-typescript-guide)

### good lessons
[Tutorial: How to set up React, webpack, and Babel 7 from scratch (2019) ](https://www.valentinog.com/blog/babel/)
[Webpack 4 Tutorial: from 0 Conf to Production Mode](https://www.valentinog.com/blog/webpack/)
[Container Components](https://medium.com/@learnreact/container-components-c0e67432e005)
[Presentational and Container Components](https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0)
[基于Webpack搭建React开发环境](https://juejin.im/post/5afc29fa6fb9a07ab379a2ae)

[Webpack 4 + React with Typescript](https://medium.com/@atingenkay/webpack-4-react-with-typescript-996eb78ff348)
https://www.typescriptlang.org/docs/handbook/react-&-webpack.html


### webpack, typescript, react

https://medium.com/@atingenkay/webpack-4-react-with-typescript-996eb78ff348
https://www.typescriptlang.org/docs/handbook/react-&-webpack.html
https://www.tslang.cn/docs/handbook/compiler-options.html
http://json.schemastore.org/tsconfig
import fails with 'no default export'  https://github.com/Microsoft/TypeScript-React-Starter/issues/8

翻译 | 开始使用 TypeScript 和 React https://juejin.im/post/595cc34ff265da6c3d6c262b

`tsconfig.json`
```json
{
  "compilerOptions": {
    "allowSyntheticDefaultImports": true,
    "esModuleInterop": true,
    "moduleResolution": "node",
    "module": "esnext",
    "jsx": "react"
  }
}



```

`package.json`
```json
{
  "name": "sometimes2019.github.io",
  "version": "1.0.0",
  "description": "share",
  "main": "index.js",
  "scripts": {
    "gen-doc-mirror": "node ./doc-mirror",
    "deploy": "npm run gen-doc-mirror",
    "build": "webpack --config webpack.config.js",
    "start": "webpack-dev-server",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "repository": {
    "type": "git",
    "url": "sometimes:sometimes2019/sometimes2019.github.io.git"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "awesome-typescript-loader": "^5.2.1",
    "clean-webpack-plugin": "^2.0.2",
    "css-loader": "^2.1.1",
    "glob": "^7.1.4",
    "html-webpack-plugin": "^3.2.0",
    "less": "^2.7.2",
    "less-loader": "^5.0.0",
    "style-loader": "^0.23.1",
    "ts-import-plugin": "^1.5.5",
    "typescript": "^3.4.5",
    "upath": "^1.1.2",
    "webpack": "^4.31.0",
    "webpack-cli": "^3.3.0",
    "webpack-dev-server": "^3.3.1"
  },
  "dependencies": {
    "@types/react": "^16.8.17",
    "@types/react-dom": "^16.8.4",
    "antd": "^3.18.1",
    "moment": "^2.24.0",
    "react": "^16.8.6",
    "react-dom": "^16.8.6"
  }
}



```

`webpack.config.js`
```js
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin')
const CleanWebpackPlugin = require('clean-webpack-plugin')
const webpack = require('webpack')
const tsImportPluginFactory = require('ts-import-plugin')

module.exports = {
  entry: {
    app: './src/index.tsx'
  },
  mode: 'development',
  resolve: {
    extensions: [".ts", ".tsx", ".js", ".json"]
  },
  output: {
    filename: '[name].bundle.js',
    path: path.resolve(__dirname, 'dist')
  },
  devtool: 'cheap-module-source-map',
  devServer: {
    contentBase: './',
    hot: true
  },
  module: {
    rules: [
      {
        test: /\.tsx?$/,
        loader: 'awesome-typescript-loader',
        options: {
          getCustomTransformers: () => ({
            before: [tsImportPluginFactory({
              libraryName: 'antd',
              libraryDirectory: 'lib',
              style: true
            })]
          })
        },
        include: /src/
      },
      {
        test: /\.css$/,
        use: ['style-loader', 'css-loader']
      },
      {
        test: /\.less$/,
        use: ['style-loader', 'css-loader', 'less-loader']
      }
    ]
  },
  plugins: [
    new CleanWebpackPlugin(),
    new HtmlWebpackPlugin({
      title: 'my tool',
      template: 'index.html'
    }),
    new webpack.HotModuleReplacementPlugin()
  ]
};


```
https://github.com/sometimes2019/sometimes2019.github.io

### 深入理解 TypeScript
https://jkchao.github.io/typescript-book-chinese/


### typescript 排错

- `vscode`中代码提示“重复函数实现”警告 Duplicate function implementation
  试试 `tsc --init`
  https://stackoverrun.com/cn/q/12144042
  https://github.com/Microsoft/TypeScript/issues/10804


### 引入第三方模块 没有type定义 d.ts 时的兼容办法

项目中创建一个`types`目录，新建一个 `index.d.ts` 文件
```ts

declare module 'my-ftp-deploy' {
  const FtpDeployer: any;
  export = FtpDeployer;
}

```
然后 `tsconfig.json` 中指定下这个模块定义的路径
```json
{
  "baseUrl": "./",
    "paths": {
      "my-ftp-deploy": ["src/@types/my-ftp-deploy"]
    },
}
```


###  tsconfig.json 指南
https://blog.csdn.net/qq_36380426/article/details/106486207

### 函数类型

```ts

function greeter(fn: (a: string) => void) {
  fn("Hello, World");
}

function printToConsole(s: string) {
  console.log(s);
}

greeter(printToConsole);


// =======

type GreetFunction = (a: string) => void;
function greeter(fn: GreetFunction) {
  // ...
}


// ========
type DescribableFunction = {
  description: string;
  (someArg: number): boolean;
};
function doSomething(fn: DescribableFunction) {
  console.log(fn.description + " returned " + fn(6));
}

// ===

type SomeConstructor = {
  new (s: string): SomeObject;
};
function fn(ctor: SomeConstructor) {
  return new ctor("hello");
}
Try






```


### 类型合并  类型组合


```ts
interface Colorful {
  color: string;
}

interface Circle {
  radius: number;
}

interface ColorfulCircle extends Colorful, Circle {}
```


```ts
interface Colorful {
  color: string;
}
interface Circle {
  radius: number;
}

type ColorfulCircle = Colorful & Circle;
```


## 接口继承与交叉类型（Interfaces vs Intersections） 区别

```ts
interface Colorful {
  color: string;
}

interface ColorfulSub extends Colorful {
  color: number
}

// Interface 'ColorfulSub' incorrectly extends interface 'Colorful'.
// Types of property 'color' are incompatible.
// Type 'number' is not assignable to type 'string'.

```


使用继承的方式，如果重写类型会导致编译错误，但交叉类型不会：

```ts
interface Colorful {
  color: string;
}

type ColorfulSub = Colorful & {
  color: number
}
```
虽然不会报错，那 color 属性的类型是什么呢，答案是 never，取得是 string 和 number 的交集。
