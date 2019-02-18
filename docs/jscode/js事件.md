### 绑定事件

```js
var addEvent = (function() {
    if (document.addEventListener) {
        return function (element, type, handler) { //这里，可以避免了重复检测
            element.addEventListener(type, handler, false);
        }
    } else if (document.attachEvent) {
        return function (element, type, handler) { //这里，可以避免了重复检测
            element.attachEvent('on' + type, handler);
        };
    }
})();
```

```js
var addEvent = function(element, type, handler) {
    if (document.addEventListener) {  //每次都要检测
        element.addEventListener(type, handler, false);
    } else if (document.attachEvent) {
        element.attachEvent('on' + type, handler);
    }
};
```

```js
// javascript与HTML之间的交互是通过事件实现的。
// 由于不同的浏览器提供了相似但不同的API。给项目开发带来很多麻烦。
// 外观模式(门面模式)，是一种相对简单而又无处不在的模式。
// 外观模式提供一个高层的简化的接口，这个接口使得客户端或子系统更加方便调用。
// 请使用外观模式实现跨浏览器事件处理
function addEvent (el, type, fn) {
  if (document.addEventListener) {
    el.addEventListener(type, fn, false);
  } else if (document.attachEvent) {
    el.attachEvent('on' + type, fn);
  } else {
    el['on' + type] = fn;
  }
}

var util = {}
util.Event = {
  getEvent: function (e) {
    return e
  },
  getTarget: function (e) {
    return e.target
  },
  stopPropagation: function (e) {
    if (e && e.stopPropagation) {
      e.stopPropagation()
    } else {
      window.event.cancelBubble = true;
    }
  },
  preventDefault: function (e) {
    if (e && e.preventDefault) {
      e.preventDefault()
    } else {
      window.event.returnValue = false;
    }
  },
  stopEvent: function (e) {
    return false;
  }
};

addEvent(document.getElementById('example'), 'click', function (e) {
  // Who clicked me.
  console.log(util.Event.getTarget(e));
  // Stop propagating and prevent the default action.
  util.Event.stopEvent(e);
});

```
