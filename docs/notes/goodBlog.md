
### 掘金翻译计划
https://github.com/xitu/gold-miner

### best-chinese-front-end-blogs ⭐️⭐️⭐️⭐️⭐️
https://github.com/FrankFang/best-chinese-front-end-blogs

### A delightful list of personal tech blogs ⭐️⭐️⭐️⭐️⭐️
https://github.com/jkup/awesome-personal-blogs

### CS-Notes 技术面试必备基础知识⭐️⭐️⭐️⭐️⭐️
https://github.com/CyC2018/CS-Notes

### 从浏览器多进程到JS单线程，JS运行机制最全面的一次梳理 ⭐️⭐️⭐️
https://juejin.im/post/5a6547d0f265da3e283a1df7

### 从输入URL到页面加载的过程？如何由一道题完善自己的前端知识体系⭐️⭐️⭐️
http://www.dailichun.com/2018/03/12/whenyouenteraurl.html

### 冴羽写博客的地方，预计写四个系列：JavaScript深入系列、JavaScript专题系列、ES6系列、React系列。⭐️⭐️⭐️⭐️
https://github.com/mqyqingfeng/Blog

[JavaScript深入之bind的模拟实现](https://github.com/mqyqingfeng/Blog/issues/12)⭐️


### oxxo
https://www.oxxostudio.tw/


###  villainhr
https://www.villainhr.com/

###  Feflow
腾讯开源的用于提升工程效率的前端工作流和规范工具
https://www.feflowjs.org/zh-cn/docs/

### Migrating from Medium to Gatsby  翻译目标⭐️⭐️⭐️
https://www.no.lol/2019-03-16-medium-to-gatsby/
https://github.com/poteto/no.lol


### A list of books 📚and articles 📝 for the discerning web developer to read. ⭐️⭐️⭐️
https://github.com/twhite96/js-dev-reads#the-problem-confused


### package.json 中的 Module 字段是干嘛的 ⭐️⭐️⭐️
https://github.com/sunyongjian/blog/issues/37

pkg.module 字段要指向的应该是一个基于 ES6 模块规范的使用ES5语法书写的模块。

基于 ES6 模块规范是为了用户在使用我们的包时可以享受 Tree Shaking 带来的好处；使用 ES5 语法书写是为了用户在配置 babel 插件时可以放心的屏蔽 node_modules 目录。

我们的 package.json 文件中看起来会是这个样子：

```json
{
  "main": "dist/dist.js",
  "module": "dist/dist.es.js"
}
```
相当于在一个包内同时发布了两种模块规范的版本。

当打包工具遇到我们的模块时：

如果它已经支持 pkg.module 字段则会优先使用 ES6 模块规范的版本，这样可以启用 Tree Shaking 机制。
如果它还不识别 pkg.module 字段则会使用我们已经编译成 CommonJS 规范的版本，也不会阻碍打包流程。

https://loveky.github.io/2018/02/26/tree-shaking-and-pkg.module/


### 前端同构渲染的思考与实践
https://mp.weixin.qq.com/s/0SYar2_08sAuwczAP9xt4Q


### Optimize your libraries with webpack

https://github.com/GoogleChromeLabs/webpack-libs-optimizations


### 孟坤
https://mkblog.cn/
在线音乐播放 https://www.jikefan.com/music/
https://lai.yuweining.cn/archives/2217/


###  吕立青
https://blog.jimmylv.info/


### chenchunyong/blog
https://github.com/chenchunyong/blog


### Yifeng Wang 雪碧

http://ewind.us/
https://github.com/doodlewind


### 蚂蚁数据体验技术团队的文章仓库
https://github.com/ProtoTeam/blog


### KiwenLau Fundebug 创始人
https://kiwenlau.com/

### Chrome插件开发 - github仓库star趋势图
https://github.com/SmallStoneSK/Blog


### MyDocs light2001 文档类项目，目前自己技术研究日常所需的文档，自己写的文档汇总
https://github.com/light2001/MyDocs


### 服务端渲染 运行流畅的博客
https://www.neroht.com/
