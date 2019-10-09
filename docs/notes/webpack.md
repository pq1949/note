### 自动生成webpack配置

https://createapp.dev

http://webpack.jakoblind.no


### webpack 教程

英文  https://webpack.js.org/concepts/

中文 https://www.webpackjs.com/concepts/


### Time-saving synchronised browser testing.
https://browsersync.io/
http://www.browsersync.cn/


### webpack sourcemap
https://blog.csdn.net/liwusen/article/details/79414508
https://segmentfault.com/a/1190000016404266


### Critical dependencies webpack WARNING
This seems to be a pre-built javascript file. Though this is possible, it's not recommended. Try to require the original source to get better results.

linux
```
 module: {
        noParse: /node_modules\/localforage\/dist\/localforage.js/,
        loaders: [...],
```

windows
```
/[\/\\]node_modules[\/\\]localforage[\/\\]dist[\/\\]localforage\.js$/
```

https://github.com/localForage/localForage/issues/577
