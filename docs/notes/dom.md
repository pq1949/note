### <link>标签的rel属性详解
  * https://www.jianshu.com/p/db82e6067e5

### HTML 页面设置不缓存

```html
<meta http-equiv="Expires" content="0">
<meta http-equiv="Pragma" content="no-cache">
<meta http-equiv="Cache-control" content="no-cache">
<meta http-equiv="Cache" content="no-cache">
```

### 设置 input 或者 textarea 选中的元素

`set​Selection​Range`

`selectionStart` `selectionEnd`

https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLInputElement/setSelectionRange


### textarea chrome中默认会有间距

可以通过 vertical-align: bottom | top; 解决

https://segmentfault.com/q/1010000003904393/a-1020000003904469


### IE的伪元素设置 `display table` 无效
https://stackoverflow.com/questions/29379602/in-ie11-using-pseudo-element-before-and-displaytable-cell-and-glyphicons-cont


### append appendChild

- ParentNode.append()允许追加  DOMString 对象，而 Node.appendChild() 只接受 Node 对象。
- ParentNode.append() 没有返回值，而 Node.appendChild() 返回追加的 Node 对象。
- ParentNode.append() 可以追加多个节点和字符串，而 Node.appendChild() 只能追加一个节点。
-  append 兼容性没有appendChild高，在微信的pc浏览器中 dom元素没有append方法， 只支持  appendChild

### document.hidden document.hasFocus()

document.hidden -> 判断页面是否可见 https://developer.mozilla.org/zh-CN/docs/Web/API/Document/hidden

document.hasFocus -> 判断页面是否被用户选中 https://developer.mozilla.org/zh-CN/docs/Web/API/Document/hasFocus
