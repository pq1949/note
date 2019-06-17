### 大文件

```js
var fs = require("fs");

let file = fs.createWriteStream("test2.txt", { flags: "a" });

let str = "";

for (let i = 0; i < 1024; i++) {
  str += "0";
}
for (let i = 0; i < 1024 * 1024 * 2; i++) {
  file.write(str);
}

file.end("end!", () => {
  console.log("end!");
});
```

### 刷新页面

- `location.reload` 类似于你浏览器上的刷新页面按钮
- `history.go(0)` 返回当前页 `history.go(-1)` 返回上一页(括号中写-2 代表返回上两页) `history.back()` 返回上一页 `history.forward()` 返回下一页
- `location=location`
- `location=location.href`
- `location.replace(location)` 用一个新文档取代当前文档 **使用 replace 方法之后，不能通过“前进”和“后退”来访问已经被替换的 URL**
- `location.replace(location.href)`
- `<meta http-equiv="refresh" content="5">` 每隔 5 秒刷新一次页面
- `<meta http-equiv="refresh" content="20;url=https://www.baidu.com">` 20 秒之后页面跳转到 baidu 中，通常运用到 404 页面`

https://www.jianshu.com/p/d8176460efc4

https://www.haorooms.com/post/js_refrash

### 绑定事件

```js
var addEvent = (function() {
  if (document.addEventListener) {
    return function(element, type, handler) {
      //这里，可以避免了重复检测
      element.addEventListener(type, handler, false);
    };
  } else if (document.attachEvent) {
    return function(element, type, handler) {
      //这里，可以避免了重复检测
      element.attachEvent("on" + type, handler);
    };
  }
})();
```

```js
var addEvent = function(element, type, handler) {
  if (document.addEventListener) {
    //每次都要检测
    element.addEventListener(type, handler, false);
  } else if (document.attachEvent) {
    element.attachEvent("on" + type, handler);
  }
};
```

```js
// javascript与HTML之间的交互是通过事件实现的。
// 由于不同的浏览器提供了相似但不同的API。给项目开发带来很多麻烦。
// 外观模式(门面模式)，是一种相对简单而又无处不在的模式。
// 外观模式提供一个高层的简化的接口，这个接口使得客户端或子系统更加方便调用。
// 请使用外观模式实现跨浏览器事件处理
function addEvent(el, type, fn) {
  if (document.addEventListener) {
    el.addEventListener(type, fn, false);
  } else if (document.attachEvent) {
    el.attachEvent("on" + type, fn);
  } else {
    el["on" + type] = fn;
  }
}

var util = {};
util.Event = {
  getEvent: function(e) {
    return e;
  },
  getTarget: function(e) {
    return e.target;
  },
  stopPropagation: function(e) {
    if (e && e.stopPropagation) {
      e.stopPropagation();
    } else {
      window.event.cancelBubble = true;
    }
  },
  preventDefault: function(e) {
    if (e && e.preventDefault) {
      e.preventDefault();
    } else {
      window.event.returnValue = false;
    }
  },
  stopEvent: function(e) {
    return false;
  }
};

addEvent(document.getElementById("example"), "click", function(e) {
  // Who clicked me.
  console.log(util.Event.getTarget(e));
  // Stop propagating and prevent the default action.
  util.Event.stopEvent(e);
});
```

### compose (redux)

```js
/**
 * Composes single-argument functions from right to left. The rightmost
 * function can take multiple arguments as it provides the signature for
 * the resulting composite function.
 *
 * @param {...Function} funcs The functions to compose.
 * @returns {Function} A function obtained by composing the argument functions
 * from right to left. For example, compose(f, g, h) is identical to doing
 * (...args) => f(g(h(...args))).
 */

export default function compose(...funcs) {
  if (funcs.length === 0) {
    return arg => arg;
  }

  if (funcs.length === 1) {
    return funcs[0];
  }

  return funcs.reduce((a, b) => (...args) => a(b(...args)));
}
```

### 纯对象判断 isPlainObject (redux)

```js
/**
 * @param {any} obj The object to inspect.
 * @returns {boolean} True if the argument appears to be a plain object.
 */
export default function isPlainObject(obj) {
  if (typeof obj !== "object" || obj === null) return false;

  let proto = obj;
  while (Object.getPrototypeOf(proto) !== null) {
    proto = Object.getPrototypeOf(proto);
  }

  return Object.getPrototypeOf(obj) === proto;
}
```

### 获取随机的字符串 (redux)

```js
Math.random()
  .toString(36)
  .substring(7);
```

### 交换数组中两个元素 (react-spring-examples)

```js
// Swaps two values in an array
const swap = (array, from, to) => (
  array.splice(to, 0, ...array.splice(from, 1)), array
);
```

### 交互两个数据

```js
// 1. 数组解构
[a, b] = [b, a];

// 2. 异或交换
a = a ^ b;
b = a ^ b;
a = a ^ b;

// 3. tem
tem = b;
b = a;
a = tem;
```

### 浏览器控制台加载脚本

```js
var __s = document.createElement("script");
__s.src = "https://cdn.bootcss.com/gpu.js/1.10.4/gpu-core.min.js";
document.getElementsByTagName("head")[0].appendChild(__s);
```

### 乱序 洗牌

https://github.com/mqyqingfeng/Blog/issues/51

```js
var values = [1, 2, 3, 4, 5];

values.sort(function() {
  return Math.random() - 0.5;
});

console.log(values);
```
