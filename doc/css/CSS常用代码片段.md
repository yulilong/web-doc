[TOC]

## 1. 高度自适应屏幕高度

例子： 网站底部的版权条，当内容不足一屏的时候显示在屏幕的底部，在内容超过一屏的时候显示在所有内容的底部。

使用flex布局：

```html
<style>
    .container { display: flex; min-height: 100vh;
        flex-direction: column;
    }
    header { background: #cecece; min-height: 100px;
    }
    content { background: #bbbbbb;
        flex: 1; /* 1 代表盡可能最大，會自動填滿除了 header footer 以外的空間 */
    }
    footer { background: #333333; min-height: 100px; }
</style>
<div class="container">
  <header></header>
  <content></content>
  <footer></footer>
</div>
```

这样`<footer>`就会在底部了。

参考资料：https://blog.csdn.net/u014374031/article/details/69258208



## 2. a标签去掉下划线



```html
<style type="text/css">
a:link,a:visited{
 text-decoration:none;  /*超链接无下划线*/
}
a:hover{
 text-decoration:underline;  /*鼠标放上去有下划线*/
}
</style>

<a href="#">超链接</a>
```



## 3. input输入框输入时去掉默认蓝边

```less
input {
    &:focus {
        outline: none;
    }
}
```



## 4. input输入框placeholder字体颜色修改

```less
input {
    &::-webkit-input-placeholder { /* WebKit browsers*/ 
        color:#999;
        font-size: 20px;
    }
    &:-moz-placeholder {  /* Mozilla Firefox 4 to 18*/ 
        color:#999;
    }
    &::-moz-placeholder {  /* Mozilla Firefox 19+*/ 
        color:#999;
    }
    &:-ms-input-placeholder { /* Internet Explorer 10+*/ 
        color:#999;
    }
}
```

## 5 div模拟textarea文本域实现高度自适应

HTML：

```html
<div class="textarea" contenteditable="true"><br /></div>
```

CSS:

```css
.textarea{
    width: 200px;
    min-height: 20px;
    max-height: 300px;
    _height: 120px;
    margin-left: auto;
    margin-right: auto;
    padding: 3px;
    outline: 0;
    border: 1px solid #a0b3d6;
    font-size: 12px;
    line-height: 24px;
    padding: 2px;
    word-wrap: break-word;
    overflow-x: hidden;
    overflow-y: auto;

    border-color: rgba(82, 168, 236, 0.8);
    box-shadow: inset 0 1px 3px rgba(0, 0, 0, 0.1), 0 0 8px rgba(82, 168, 236, 0.6);
}
```

## 6 input复选框CheckBox默认演示纯CSS修改

HTML：

```html
<input type="checkbox" name="btn" id="btn1"><label for="btn1">按钮2</label>
```

CSS:

```css
input[type="checkbox"]{
  width:20px;
  height:20px;
  display: inline-block;
  text-align: center;
  vertical-align: middle; 
  line-height: 18px;
  position: relative;
}
input[type="checkbox"]::before{
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  background: #fff;
  width: 100%;
  height: 100%;
  border: 1px solid #d9d9d9;
}
input[type="checkbox"]:checked::before{
  content: "\2713";  // “\2713”实体符号√
  background-color: #fff;
  position: absolute;
  top: 0;
  left: 0;
  width:100%;
  border: 1px solid #e50232;
  color:#e50232;
  font-size: 20px;
  font-weight: bold;
}
```

## 7 禁止文字被选中

HTML：

```html
<div class="tt">你好，测试禁止选中文本</div>
```

CSS:

```css
.tt {
   -o-user-select: none;
  -moz-user-select: none; /*火狐 firefox*/
  -webkit-user-select: none; /*webkit浏览器*/
  -ms-user-select: none; /*IE10+*/
  -khtml-user-select :none; /*早期的浏览器*/
  user-select: none; 
}
```

user-select有四个值：

> none：文本不能被选择
>
> text：可以选择文本
>
> all：当所有内容作为一个整体时可以被选择。如果双击或者在上下文上点击子元素，那么被选择的部分将是以该子元素向上回溯的最高祖先元素。
>
> element：可以选择文本，但选择范围受元素边界的约束

值得注意的是：IE6-9目前需要通过JavaScript来实现。

```javascript
document.body.onselectstart = document.body.ondrag = function(){
  return false;
}
```

参考资料：https://blog.csdn.net/qq_39241443/article/details/79533898

## 8. 隐藏页面元素几种方法

1、**display:none** 

```css
.hidden{
    display:none
}
```

将元素设置为`display:none`后，元素在页面上将彻底消失，元素本来占有的空间就会被其他元素占有，也就是说它会导致浏览器的重排和重绘。

此方法有时可能会导致前端框架里面找不到这个元素。

2、visibility:hidden

```css
.hidden{
    visibility:hidden
}
```

此方法也是一种常用的隐藏元素的方法，和`display:none`的区别在于，元素在页面消失后，其占据的空间依旧会保留着，所以它只会导致浏览器重绘而不会重排

`visibility:hidden`适用于那些元素隐藏后不希望页面布局会发生变化的场景

3、**opacity:0** 

```css
.hidden {
    opacity:0;
}
```

`opacity`属性表示元素的透明度，而将元素的透明度设置为0后，在我们眼中，元素也就是隐藏起来的，这也算是一种隐藏元素的方法

这种方法和`visibility:hidden`的一个共同点是元素隐藏后依旧占据着空间，但我们都知道，设置透明度为0后，元素只是隐身了，它依旧存在页面中

4、设置height、width等盒模型属性为0

将元素的`margin，border，padding，height`和`width`等影响元素盒模型的属性设置成0，如果元素内有子元素或内容，还应该设置其`overflow:hidden`来隐藏其子元素

```css
.hidden {
    margin:0; border:0; padding:0;
    height:0; width:0;
    overflow:hidden;
}
```

`jquery`的`slideUp`动画，它就是设置元素的`overflow:hidden`后，接着通过定时器，不断地设置元素的`height，margin-top，margin-bottom，border-top，border-bottom，padding-top，padding-bottom`为0，从而达到`slideUp`的效果

### 8.1 元素隐藏后的事件响应

```html
<style>
    div {
        width: 100px;
        height: 100px;
        background: red;
        margin: 15px;
        padding: 10px;
        border: 5px solid green;
        display: inline-block;
        overflow: hidden;
    }
    .none { display: none; }
    .hidden { visibility: hidden; }
    .opacity0 { opacity: 0; }
    .height0 { height: 0; }
</style>

<div class="none"></div>
<div class="hidden"></div>
<div class="opacity0"></div>
<div class="height0">aa</div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.0.0/jquery.min.js"></script>
<script>
    $(".none").on("click", function () {
        console.log("none clicked");
    })
    $(".hidden").on("click", function () {
        console.log("hidden clicked");
    })
    $(".opacity0").on("click", function () {
        console.log("opacity0 clicked");
    })
    $(".height0").on("click", function () {
        console.log("height0 clicked");
    })
</script>

```

这段代码将四种隐藏元素的方法分别展示出来，然后绑定其点击事件，经过测试，主要有下面的结论：

这段代码将四种隐藏元素的方法分别展示出来，然后绑定其点击事件，经过测试，主要有下面的结论：

> - `display:none`:元素彻底消失，很显然不会触发其点击事件
> - `visibility:hidden`:无法触发其点击事件，有一种说法是`display:none`是看不见摸不着，而`visibility:hidden`是看不见摸得着，这种说法是不准确的，设置元素的`visibility`后无法触发点击事件，说明这种方法元素也是消失了，只是依然占据着页面空间
> - `opacity:0`:可以触发点击事件，原因也很简单，设置元素透明度为0后，元素只是相对于人眼不存在而已，对浏览器来说，它还是存在的，所以可以触发点击事件
> - `height:0`:将元素的高度设置为0，并且设置overflow:hidden。使用这种方法来隐藏元素，是否可以触发事件要根据具体的情况来分析。如果元素设置了`border，padding`等属性不为0，很显然，页面上还是能看到这个元素的，触发元素的点击事件完全没有问题。如果全部属性都设置为0，很显然，这个元素相当于消失了，即无法触发点击事件

但是这些结论真的准确吗？
我们在上面的代码中添加这样一句代码：`$(".none").click()`
结果发现，触发了`click`事件，也就是通过JS可以触发被设置为`display:none`的元素的事件。
所以前面无法触发点击事件的真正原因是鼠标无法真正接触到被设置成隐藏的元素

### 8.2 CSS3 transition对这几种方法的影响

`CSS3`提供的`transition`极大地提高了网页动画的编写，但并不是每一种`CSS`属性都可以通过`transition`来进行动画的。我们修改代码如下：

```html
<style>
    div {
        width: 100px;
        height: 100px;
        background: red;
        margin: 15px;
        padding: 10px;
        border: 5px solid green;
        display: inline-block;
        overflow: hidden;
        transition: all linear 2s;
    }
</style>

<div class="none"></div>
<div class="hidden"></div>
<div class="opacity0"></div>
<div class="height0">aa</div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.0.0/jquery.min.js"></script>
<script>
$(".none").on("click", function () {
    console.log("none clicked");
    $(this).css("display", "none");
})
$(".hidden").on("click", function () {
    console.log("hidden clicked");
    $(this).css("visibility", "hidden");
})
$(".opacity0").on("click", function () {
    console.log("opacity0 clicked");
    $(this).css("opacity", 0);
})
$(".height0").on("click", function () {
    console.log("height0 clicked");
    $(this).css({
        "height": 0,
    });
})
</script>
```

经过测试，可以看到：

> - `display:none`:完全不受`transition`属性的影响，元素立即消失
> - `visibility：hidden`:元素消失的时间跟`transition`属性设置的时间一样，但是没有动画效果
> - `opacity`和`height`等属性能够进行正常的动画效果

假设我们要通过CSS3来做一个淡出的动画效果，应该如下：

```css
.fadeOut { visibility: visible; opacity: 1; transition: all linear 2s; }
.fadeOut:hover { visibility: hidden; opacity: 0; }
```

应该同时设置元素的`visibility`和`opacity`属性

参考资料：https://segmentfault.com/a/1190000007542357