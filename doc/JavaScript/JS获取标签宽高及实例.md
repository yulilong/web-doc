[TOC]



## 1. 常用的获取宽高的属性



```javascript
// 1. 获取屏幕的高度和宽度(屏幕分辨率):
window.screen.height 		// 1440
window.screen.width			// 2560

// 2. 获取浏览器相对于屏幕距离
window.screenTop; 			//  浏览器上面距离屏幕顶部距离
window.screenLeft;			// 浏览器左边距离屏幕左边的距离

// 2. 获取屏幕工作区域的高度和宽度（去掉状态栏）：
window.screen.availHeight  	// 1363
window.screen.availWidth 	// 2560

// 3. 网页全文的高度和宽度：
document.body.scrollHeight	// 9969
document.body.scrollWidth 	// 1124

// 4. 滚动条卷上去的高度和向右卷的宽度：body和documentElement有一个是有效的
document.body.scrollTop  	// 0 : 如果body没有滚动条则为0
document.body.scrollLeft 
document.documentElement.scrollTop	
document.documentElement.scrollLeft

// 5. 网页可见区域的高度和宽度（不加边线）：
document.body.clientHeight  // 9969
document.body.clientWidth 	// 845
document.documentElement.clientHeight
document.documentElement.lientWidth

// 6. 网页可见区域的高度和宽度（加边线）：
document.body.offsetHeight 	// 9969
document.body.offsetWidth	// 845
```



## 2. 关于offset的5个属性

### 2.1 offsetWidth与offsetHeight

元素的offsetWidth：元素的IE盒模型的宽度

元素的offsetHeight：元素的IE盒模型的高度

![](http://ww1.sinaimg.cn/large/005M7QYPly1fj8v8kad8yj30bf06vaan.jpg)

### 2.3 offsetLeft与offsetTop

**HTMLElement.offsetLeft**:只读属性，返回当前元素*左上角*相对于  [`HTMLElement.offsetParent`](https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLElement/offsetParent) 节点的左边界偏移的像素值

**HTMLElement.offsetTop** 只读属性，它返回当前元素相对于其 [`offsetParent`](https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLElement/offsetParent) 元素的顶部的距离。



### 2.4 offsetParent

1. 如果当前元素的父级元素没有进行CSS定位（position为absolute或relative），则 `offsetParent` 为最近的 `table`, `table cell` 或根元素（标准模式下为 `html`；quirks 模式下为 `body`）。
2. 如果当前元素的父级元素中有CSS定位（position为absolute或relative），offsetParent取最近的那个父级元素。
3. `offsetParent` 很有用，因为 [`offsetTop`](https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLElement/offsetTop) 和 [`offsetLeft`](https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLElement/offsetLeft) 都是相对于其内边距边界的。



## 3. 关于宽高的实际应用

### 3.1 判断滚动条到底的条件

scrollTop + clientHeight == scrollHeight

```javascript
// 已经滚动了多少距离
function getScrollTop(){
　　var scrollTop = 0, bodyScrollTop = 0, documentScrollTop = 0;
　　if(document.body){ bodyScrollTop = document.body.scrollTop; }
　　if(document.documentElement){
　　　　documentScrollTop = document.documentElement.scrollTop;
　　}
　　scrollTop = (bodyScrollTop - documentScrollTop > 0) ? bodyScrollTop : documentScrollTop;
　　return scrollTop;
}
//文档的总高度
function getScrollHeight(){
　　var scrollHeight = 0, bodyScrollHeight = 0, documentScrollHeight = 0;
　　if(document.body){ bodyScrollHeight = document.body.scrollHeight; }
　　if(document.documentElement){
　　　　documentScrollHeight = document.documentElement.scrollHeight;
　　}
　　scrollHeight = (bodyScrollHeight - documentScrollHeight > 0) ? bodyScrollHeight : documentScrollHeight;
　　return scrollHeight;
}
// 获取浏览器可见部分的高度
function getWindowHeight(){
　　var windowHeight = 0;
　　if(document.compatMode == "CSS1Compat"){
　　　　windowHeight = document.documentElement.clientHeight;
　　}else{ windowHeight = document.body.clientHeight; }
　　return windowHeight;
}
// 绑定滚动事件
window.onscroll = function(){
　　if(getScrollTop() + getWindowHeight() == getScrollHeight()){
　　　　console.log("已经到最底部了！!");
　　}
};

//jquery 实现
$(window).scroll(function(){
　　var scrollTop = $(this).scrollTop();
　　var scrollHeight = $(document).height();
　　var windowHeight = $(this).height();
　　if(scrollTop + windowHeight == scrollHeight){
　　　　console.log("已经到最底部了！");
　　}
});
```



### 3.2 JS判断div内离开顶部， 设置滚动到指定位置， 判断滚动到达底部：

```html
<style>
    body { margin: 0; }
    .one { border: 1px solid; height: 300px; width: 300px;
      overflow: scroll; position: relative;
    }
    p { margin: 30px 0; border: 1px solid red; }
  </style>
  <p>123</p><p>9999</p>
  <div class="one">
    <p>1</p><p>2</p><p>3</p> <p>4</p><p>5</p><p>6</p>
    <p>7</p><p>8</p><p>9</p> <p>10</p><p>11</p><p>12</p>
    <p>13</p><p class=f>ffffffffffffffffffffffffff</p><p>14</p>
    <p>15</p><p>16</p><p>17</p> <p>18</p><p>19</p><p>20</p>
  </div>
  <script>
      var one = document.querySelector(".one");
      var f = document.querySelector(".f");
      // one.scrollTop = f.offsetTop;	设置 直接滚动到指定位置
      var leave = false;
      var fflag = false;	// 判断是否已经出发了条件
      one.onscroll = function() {
          console.log(f.offsetTop)
          if (this.scrollTop > 0 && leave === false){
              console.log('离开顶部了'); leave = true;
          }
          if (this.scrollTop === 0 && leave === true) {
              console.log('在顶部了'); leave = false;
          }
          if (this.scrollTop + this.clientHeight === this.scrollHeight) {
              console.log('到底部了');
          }
          if (this.scrollTop > f.offsetTop && !fflag) {
            console.log('到达指定位置了');
            fflag = true; // 过了指定位置后，关闭指定提示， 
          }
          // 小于指定位置后，从新打开指定位置
          if (this.scrollTop < f.offsetTop  && fflag) {
            fflag = false;
          }
      }
      console.log(f.offsetTop)
  </script>
```



## 4. document.compatMode对获取浏览器窗口大小的影响

document.compatMode用来判断当前浏览器采用的渲染方式。

IE对盒模型的渲染在 Standards Mode和Quirks Mode是有很大差别的：

> Standards Mode：盒模型的解释和其他的标准浏览器是一样
>
> Quirks Mode: 使用IE盒模型，在不声明Doctype的情况下，IE默认Quirks Mode

而document.compatMode可以判断使用了哪种方式，它有两个值：

> BackCompat: 标准兼容模式关闭，Quirks Mode,即使用了IE盒模型：width = border + padding + content
>
> CSS1Compat：标准兼容模式开启，Standards Mode，即使用了标准盒模型: width: content

### 4.1 BackCompat： 浏览器高度使用body的值

**BackCompat：**标准兼容模式关闭，当document.compatMode等于BackCompat时，浏览器客户区宽度为document.body.clientWidth;

### 4.2 CSS1Compat：浏览器高度使用documentElement的值

**CSS1Compat：**标准兼容模式开启,当document.compatMode等于CSS1Compat时浏览器客户区宽度为document.documentElement.clientWidth;

### 4.3 DOCTYPE 会影响document.compatMode

当文档有了标准声明时， document.compatMode 的值就等于 "CSS1compat"， 因此， 我们可以根据 document.compatMode 的值来判断文档是否加了标准声明

```javascript
// HTML文件头部没有 <!DOCTYPE html>
document.compatMode	// BackCompat
// HTML文件头部有 <!DOCTYPE html>
document.compatMode	// CSS1Compat
```

### 4.4 documentElement和body 

body是DOM对象里的body子节点，即 `<body>` 标签；

documentElement 是整个节点树的根节点root，即`<html> `标签；



## 5. 浏览器兼容性问题

### 5.1 各浏览器下 scrollTop的差异

https://segmentfault.com/a/1190000008065472

**IE6/7/8：**
可以使用 `document.documentElement.scrollTop`； 
**IE9及以上：**
可以使用`window.pageYOffset`或者`document.documentElement.scrollTop `
**Safari:** 
safari： `window.pageYOffset` 与document.body.scrollTop都可以； 
**Firefox:** 
火狐等等相对标准些的浏览器就省心多了，直接用window.pageYOffset 或者 `document.documentElement.scrollTop `；
**Chrome：**
谷歌浏览器只认识`document.body.scrollTop`;
注：标准浏览器是只认识documentElement.scrollTop的，但chrome虽然我感觉比firefox还标准，但却不认识这个，在有文档声明时，chrome也只认识document.body.scrollTop.

document.body.scrollTop与document.documentElement.scrollTop两者有个特点，就是同时只会有一个值生效。

为了兼容，不管有没有 DTD，可以使用如下代码：

```javascript
var scrollTop = window.pageYOffset  //用于FF
                || document.documentElement.scrollTop  
                || document.body.scrollTop || 0;
```

**documentElement 和 body 相关说明：**

body是DOM对象里的body子节点，即 <body> 标签；

documentElement 是整个节点树的根节点root，即<html> 标签；

## 一些问题

### 1. document.body.scrollTop总是0的原因

[document.body.scrollTop与document.documentElement.scrollTop兼容](https://blog.csdn.net/lploveme/article/details/7011174)

[JS基础篇-- body.scrollTop与documentElement.scrollTop](http://www.cnblogs.com/boyuguoblog/p/7744747.html)

当判断页面滚动的时候，使用document.body.scrollTop发现页面滚动时总是返回0，经查找：

页面指定了DTD，即指定了DOCTYPE时，使用document.documentElement。

页面没有DTD，即没指定DOCTYPE时，使用document.body。

IE和Firefox都是如此。

但document.body.scrollTop与document.documentElement.scrollTop同时只会有一个值生效。比如document.body.scrollTop能取到值的时候，document.documentElement.scrollTop就会始终为0；反之亦然。所以，如果要得到网页的真正的scrollTop值，可以这样：

`var sTop=document.body.scrollTop+document.documentElement.scrollTop;`      

也可以使用下面的函数：

```javascript
function getScrollTop() {
    var scrollTop;
    if (typeof window.pageYOffset != 'undefined'){
        scrollTop = window.pageYOffset; 
    } else if (typeof document.compatMode != 'undefined' &&    document.compatMode != 'BackCompat') {
        scrollTop = document.documentElement.scrollTop;
    } else if (typeof document.body != 'undefined') {
        scrollTop = document.body.scrollTop; 
    }
    return scrollTop;
}
console.log(getScrollTop())
```



### 2. 给body标签设置高度后，显示的效果是一实际高度算的





## 参考资料



[JS如何判断滚动条是否滚到底部](http://www.cnblogs.com/yangwang12345/p/7798084.html)

[HTMLElement.offsetLeft  MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLElement/offsetLeft)

[HTMLElement.offsetParent  MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLElement/offsetParent) 

[HTML 获取屏幕、浏览器、页面的高度宽度](http://www.cnblogs.com/polk6/p/5051935.html)

[document.compatMode介绍](http://www.cnblogs.com/fullhouse/archive/2012/01/17/2324706.html)

[获取scrollTop兼容各浏览器的方法，以及body和documentElement是啥？](http://www.cnblogs.com/xwgli/p/3490466.html)

[网址在线测试  JSBIN](http://js.jirengu.com/?html,console,output)

一张了解元素宽高的图：

![](https://gss0.baidu.com/9vo3dSag_xI4khGko9WTAnF6hhy/zhidao/wh%3D600%2C800/sign=3ef1ef0370cf3bc7e855c5eae1309699/3801213fb80e7bec0d1f10ef2f2eb9389a506bf2.jpg)