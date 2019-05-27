### typescript 学习资料
https://github.com/typescript-cheatsheets/react-typescript-cheatsheet
https://basarat.gitbooks.io/typescript/content/docs/getting-started.html

Practical Advanced TypeScript https://egghead.io/courses/practical-advanced-typescript

Use Types Effectively in TypeScript https://egghead.io/courses/use-types-effectively-in-typescript


What are the best resources for learning TypeScript? Asking for a friend. @resource
https://twitter.com/mjackson/status/1128500194000220166


awesome-typescript
https://github.com/semlinker/awesome-typescript

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
