## CSS w3c 规范

[Cascading Style Sheets Level 2 Revision 1 (CSS 2.1) Specification](https://www.w3.org/TR/2011/REC-CSS2-20110607/#minitoc)

## 参考链接

### Tailwind Box Shadows css 参考

- https://tailwindcss.com/docs/shadows

### CSS Weekly

- https://css-weekly.com/archives/

### 30-seconds-of-css ⭐️⭐️⭐️⭐️

https://github.com/30-seconds/30-seconds-of-css

### QiShaoXuan css_tricks css tricks⭐️⭐️⭐️⭐️

https://qishaoxuan.github.io/css_tricks/

### flex 练习 ⭐️⭐️

https://pq1949.github.io/learn-css/flex%E7%BB%83%E4%B9%A0.html

## CSS 基础

### HTML 常见元素

![css](/../imgs/css1.png)

### 移动端布局

[使用 hotcss 可以让移动端布局开发更容易](http://imochen.github.io/hotcss/)
https://github.com/imochen/hotcss

rem

```js
  <script>!function(a,b){function c(){var b=f.getBoundingClientRect().width;b/i>540&&(b=540*i);var c=b/10;f.style.fontSize=c+"px",k.rem=a.rem=c}var d,e=a.document,f=e.documentElement,g=e.querySelector('meta[name="viewport"]'),h=e.querySelector('meta[name="flexible"]'),i=0,j=0,k=b.flexible||(b.flexible={});if(g){console.warn("将根据已有的meta标签来设置缩放比例");var l=g.getAttribute("content").match(/initial\-scale=([\d\.]+)/);l&&(j=parseFloat(l[1]),i=parseInt(1/j))}else if(h){var m=h.getAttribute("content");if(m){var n=m.match(/initial\-dpr=([\d\.]+)/),o=m.match(/maximum\-dpr=([\d\.]+)/);n&&(i=parseFloat(n[1]),j=parseFloat((1/i).toFixed(2))),o&&(i=parseFloat(o[1]),j=parseFloat((1/i).toFixed(2)))}}if(!i&&!j){var p=(a.navigator.appVersion.match(/android/gi),a.navigator.appVersion.match(/iphone/gi)),q=a.devicePixelRatio;i=p?q>=3&&(!i||i>=3)?3:q>=2&&(!i||i>=2)?2:1:1,j=1/i}if(f.setAttribute("data-dpr",i),!g)if(g=e.createElement("meta"),g.setAttribute("name","viewport"),g.setAttribute("content","initial-scale="+j+", maximum-scale="+j+", minimum-scale="+j+", user-scalable=no, viewport-fit=cover"),f.firstElementChild)f.firstElementChild.appendChild(g);else{var r=e.createElement("div");r.appendChild(g),e.write(r.innerHTML)}a.addEventListener("resize",function(){clearTimeout(d),d=setTimeout(c,300)},!1),a.addEventListener("pageshow",function(a){a.persisted&&(clearTimeout(d),d=setTimeout(c,300))},!1),"complete"===e.readyState?e.body.style.fontSize=12*i+"px":e.addEventListener("DOMContentLoaded",function(){e.body.style.fontSize=12*i+"px"},!1),c(),k.dpr=a.dpr=i,k.refreshRem=c,k.rem2px=function(a){var b=parseFloat(a)*this.rem;return"string"==typeof a&&a.match(/rem$/)&&(b+="px"),b},k.px2rem=function(a){var b=parseFloat(a)/this.rem;return"string"==typeof a&&a.match(/px$/)&&(b+="rem"),b}}(window,window.lib||(window.lib={}));</script>
```

### 不受控制的 position:fixed

当元素祖先的 transform 属性非 none 时，容器由视口改为该祖先

1. transform 属性值不为 none 的元素
2. perspective 值不为 none 的元素
3. 在 will-change 中指定了任意 CSS 属性
4. filter 属性不为 none

经过测试发现，在 MAC 下的 Safari 浏览器（WebKit 内核，Version 9.1.2 (11601.7.7)）和 IE Trident/ 内核及 Edge 浏览器下，上述三种方式都不会改变 position: fixed 的表现！

https://developer.mozilla.org/zh-CN/docs/Web/CSS/position

https://www.cnblogs.com/coco1s/p/7358830.html

https://codepen.io/Chokcoco/pen/wqXZXd

### BFC

https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Block_formatting_context

### 探秘 flex 上下文中神奇的自动 margin

- 水平垂直居中最简单的方法

```html
<div class="g-container">
  <div class="g-box"></div>
</div>
```
```cs
.g-container {
    width: 100vw;
    height: 100vh;

    display: flex;
    // display: grid;
    // display: inline-flex;
    // display: inline-grid;
}

.g-box {
    width: 40vmin;
    height: 40vmin;
    background: #000;

    margin: auto;
}
```
https://codepen.io/Chokcoco/pen/GarPev


https://juejin.im/post/5ce60afde51d455ca04361b1?utm_source=gold_browser_extension
