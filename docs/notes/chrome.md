### Command Line API 参考

`$0、$1、$2、$3 、 $4 `命令用作在 Elements 面板中检查的最后五个 DOM 元素或在 Profiles 面板中选择的最后五个 JavaScript 堆对象的历史参考。$0 返回最近一次选择的元素或 JavaScript 对象，$1 返回仅在最近一次之前选择的元素或对象，依此类推。

`$_` 返回最近评估的表达式的值。

`$(selector)` 返回带有指定的 CSS 选择器的第一个 DOM 元素的引用。此函数等同于 `document.querySelector()` 函数。

`$$(selector)` 返回与给定 CSS 选择器匹配的元素数组。此命令等同于调用 `document.querySelectorAll()`

`debug(function)` 调用指定的函数时，将触发调试程序，并在 Sources 面板上使函数内部中断，从而允许逐行执行代码并进行调试。

使用 `undebug(fn)` 停止函数中断，或使用 UI 停用所有断点。

`getEventListeners(object)` 返回在指定对象上注册的事件侦听器。返回值是一个对象，其包含每个注册的事件类型（例如，“click”或“keydown”）数组。每个数组的成员是描述为每个类型注册的侦听器的对象。例如，下面列出了在文档对象上注册的所有事件侦听器：


`monitor(function)` 调用指定函数时，系统会向控制台记录一条消息，其中指明函数名称及在调用时传递到该函数的参数
```js
 function sum(x, y) {
        return x + y;
    }
    monitor(sum);
```

使用 `unmonitor(function)` 停止监控。

`monitorEvents(object[, events])` 当在指定对象上发生一个指定事件时，将 Event 对象记录到控制台。您可以指定一个要监控的单独事件、一个事件数组或一个映射到预定义事件集合的常规事件“类型”
`monitorEvents(window, "resize");`




https://developers.google.com/web/tools/chrome-devtools/console/command-line-reference


### chrome 插件
https://developers.chrome.com/extensions/

1. [chrome插件开发 - tab选项卡管理器](https://github.com/SmallStoneSK/Blog/issues/11)
2. [chrome插件开发 - github仓库star趋势图](https://github.com/SmallStoneSK/Blog/issues/10)
3. [Chrome 插件，查看开源中国软件更新资讯](https://github.com/jaywcjlove/oscnews)
