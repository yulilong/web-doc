[TOC]

# Transition、Transform和Animation

这三个属性都是CSS3版本的属性，所以会有兼容性问题。

## 1. Transition:过度

过渡`transition`是一个复合属性，包括`transition-property`,`transition-duration`，`transition-timing-function`，`transtion-delay`四个子属性。通过四个子属性配合完成过度效果。

Internet Explorer 10、Firefox、Opera 和 Chrome 支持 transition 属性。
Safari 支持替代的 -webkit-transition 属性。
注释：Internet Explorer 9 以及更早版本的浏览器不支持 transition 属性。

### 1.1 transition-property:过渡的属性
  过渡的属性的名称，比如 transition-property:backgrond 就是指 backgound 参与这个过渡
  值：none(没有指定任何样式)、 all(默认值，指定元素所有支持transition-property属性的样式)、` <transition-property>`(可选过度样式)
  适用于：所有元素
  继承性：无

不是所有的CSS样式都可以过渡，只有具有中间值的属性才有过渡效果。

```
颜色：color background-color border-color outline-color
位置：background-position left right top botton
长度：
    [1]max-height min-height max-width min-width height width
    [2]border-width margin padding outline-width outline-offset
    [3]font-size line-height text-indent vertical-align  
    [4]border-spacing letter-spacing word-spacing
数字: opacity visibility z-index font-weight zoom
组合: text-shadow transform box-shadow clip
其他: gradient
```



### 1.2 transition-duration:过渡持续时间

定义过渡效果花费的时间,默认是 0
该属性单位是 秒（s）或者毫秒（ms），该属性必须带单位，如果为0s则为默认值，如为0则为无效值。
该值为单值时，所有的过渡属性都对应同样时间；该值为多值时，过渡属性按照顺序对应顺序时间

### 1.3 transition-timing-function:过渡时间函数

规定过渡效果的时间曲线,用于指定过渡类型，
初始值ease，

  ```
  ease:开始和结束慢，中间快。
  linear：匀速
  ease-in：开始慢
  ease-out: 结束慢
  ease-in-out：和ease类似，但比ease幅度大
  step-start:直接位于结束处
  step-end:位于开始处经过时间间隔后结束。
  ```

### 1.4 transition-delay:过渡延迟时间
规定过渡效果何时开始。默认值是 0s。用于制定延迟过渡的时间，该属性单位是秒（s）或毫秒（ms）

**【注意】**该属性必须带单位，0s为默认值，0则为无效值。若该属性为负值，无延迟效果，但过渡元素的起始值将从0变成设定值（*设定值=延迟时间+持续时间*），若该设定值小于等于0；则无过渡效果；若该设定值大于0，则过渡元素从该设定值开始完成剩余的过渡效果

### 1.5 实际代码例子

```less
 .box {
  width: 100px;
  height: 100px;
  background: red;
  transition: width 2s;
  -weikit-transition: width 2s; /* Safari*/
}
.box:hover {
  width: 400px;
}
```

上面的代码在鼠标放入后div的宽会在2秒内变宽到400px。

[在线代码](http://js.jirengu.com/xadub/1/edit)

其他用法

```less
/* 设置不同的transition-property，对应的transition-delay，transition-timing-function，transition-duration的属性相同时，设置一个即可。*/
.test1 {
  transition-property:width,background;
  transition-duration:3s;
  transition-timing-function:ease;
  transition-delay:500ms;
}
/*相当于*/
.test1 {
  transition:width 3s ease 500ms,background 3s ease 500ms;
}

/* 当transition-property的值的个数多余对应的其他属性时（属性值大于1个），则按顺序取值。*/
.test{
  transition-property:width,background,opacity;
  transition-duration:2s,500ms;
  transition-timing-function:linera,ease;
  transition-delay:200ms,4s;
}
/*相当于*/
.test1{
  transition:width 2s linera 200ms, background 500ms ease 4s,opacity 2s linera 200ms;
}

// 当transition-property值的个数少于对应的其他属性，则多余的属性无效。
.test1{
    transition-property: width;
    transition-duration: 2s,500ms;
    transition-timing-function: linear,ease;
    transition-delay: 200ms,0s;
}
/*类似于*/
.test1{
    transition: width 2s linear 200ms;
}

// 当transition-property的值中出现一个无效值，它依然按顺序对transition的其他属性值（其他属性出现无效值，处理情况也类似）
.test1{
    transition-property: width,wuxiao,background;
    transition-duration: 2s,500ms;
    transition-timing-function: linear,ease;
    transition-delay: 200ms,0s;
}
/*类似于*/
.test2{
    transition: width 2s linear 200ms,background 2s linear 200ms;
}

// 当transition-property的值中，有些值重复出现多次，则以最后出现的值为准，前面所有出现的值都被认定为无效值，但依然按顺序对应transition的其他属性值
.test1{
    transition-property: width,width,background;
    transition-duration: 2s,500ms;
    transition-timing-function: linear,ease;
    transition-delay: 200ms,0s;
}
/*类似于*/
.test2{
    transition: width 500ms ease 0s,background 2s linear 200ms;
}

```

参考资料：https://www.jianshu.com/p/5dbeeb2159e8

## 2. Transform:变形

参考资料：https://www.cnblogs.com/aspnetjia/p/5139020.html

指拉伸，压缩，旋转，偏移等等一些图形学里面的基本变换。这是通过修改CSS视觉格式化模型的坐标空间来实现的。

只能转换由盒子模型定位的元素。根据经验，如果元素具有`display: block`，则由盒模型定位元素。

`skew`是倾斜，`scale`是缩放，`rotate`是旋转，`translate`是平移。最后需要说明一点，transform 支持综合变换。

以如下代码为例，讲解这几个属性作用：

```html
<style>
    .one {
        width: 200px;
        height: 200px;
        background-color: red;
        transition: transform 1s linear;
    }
</style>
<div class="one"></div>
```

### 2.1 旋转:rotate

```CSS
.one:hover {
  transform: rotate(45deg);
}
```

共一个参数“角度”，单位deg为度的意思，正数为顺时针旋转，负数为逆时针旋转，上述代码作用是顺时针旋转45度。

### 2.2 缩放:scale

```less
.one:hover {
  transform: scale(0.5);
  // transform: scale(0.5, 2); 或者这样用
}
```

参数表示缩放倍数；

- 一个参数时：表示水平和垂直同时缩放该倍率
- 两个参数时：第一个参数指定水平方向的缩放倍率，第二个参数指定垂直方向的缩放倍率。

### 2.3 倾斜:skew

用法：

```less
.one:hover {
  /* transform: skewX(30deg);  X轴(水平)倾斜30度*/
  /* transform: skewy(30deg); Y轴(垂直)倾斜30度*/
  transform: skew(30deg); /* X轴(水平)倾斜30度 */
  /* transform: skew(30deg, 30deg); X轴(水平)倾斜30度, Y轴(垂直)倾斜30度*/ 
}
```

参数表示倾斜角度，单位deg

- 一个参数时：表示水平方向的倾斜角度；
- 两个参数时：第一个参数表示水平方向的倾斜角度，第二个参数表示垂直方向的倾斜角度。

### 2.4 移动:translate

用法：

```less
.one:hover {
  /* transform: translate(45px); 水平右移45px*/
  /* transform: translate(45px, 45px); 水平右移45px, 垂直下移45px*/
  /* transform: translateX(45px); 水平右移45px*/
  transform: translateY(45px); /* 垂直下移45px*/
}
```

参数表示移动距离，单位px，

- 一个参数时：表示水平方向的移动距离；
- 两个参数时：第一个参数表示水平方向的移动距离，第二个参数表示垂直方向的移动距离。

### 2.5 基准点: transform-origin

在使用transform方法进行文字或图像的变形时，是以元素的中心点为基准点进行的。使用transform-origin属性，可以改变变形的基准点。

```less
.one:hover {
  transform-origin: 10px 10px;
}
```

共两个参数，表示相对左上角原点的距离，单位px，第一个参数表示相对左上角原点水平方向的距离，第二个参数表示相对左上角原点垂直方向的距离；

两个参数除了可以设置为具体的像素值，其中第一个参数可以指定为left、center、right，第二个参数可以指定为top、center、bottom。

### 2.6 多个方法组合使用

用法：

```less
.one:hover {
  transform: rotate(45deg) scale(0.5) skew(30deg, 30deg) translate(100px, 100px);
}
```

这四种变形方法顺序可以随意，但不同的顺序导致变形结果不同，原因是变形的顺序是从左到右依次进行，这个用法中的执行顺序为1.rotate  2.scalse  3.skew  4.translate



## 3. Animation:动画

**CSS animations** 使得可以将从一个CSS样式配置转换到另一个CSS样式配置。

动画包括两个部分:

- 描述动画的样式规则
- 用于指定动画开始、结束以及中间点样式的关键帧。

相较于传统的脚本实现动画技术，使用CSS动画有三个主要优点：

1. 能够非常容易地创建简单动画，你甚至不需要了解JavaScript就能创建动画。
2. 动画运行效果良好，甚至在低性能的系统上。渲染引擎会使用跳帧或者其他技术以保证动画表现尽可能的流畅。而使用JavaScript实现的动画通常表现不佳（除非经过很好的设计）。
3. 让浏览器控制动画序列，允许浏览器优化性能和效果，如降低位于隐藏选项卡中的动画更新频率。

### 3.1 @keyframes:关键帧

[CSS3中的关键帧 MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/@keyframes)

@keyframes是定义动画的表现，通过使用[`@keyframes`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/@keyframes)建立两个或两个以上关键帧来实现。每一个关键帧都描述了动画元素在给定的时间点上应该如何渲染。

因为动画的时间设置是通过CSS样式定义的，关键帧使用百分比来指定动画发生的时间点。`0%`表示动画的第一时刻，`100%`表示动画的最终时刻。因为这两个时间点十分重要，所以还有特殊的别名：`from`和`to`。这两个都是可选的，若`from/0%`或`to/100%`未指定，则浏览器使用计算值开始或结束动画。

也可包含额外可选的关键帧，描述动画开始和结束之间的状态。您可以按任意顺序列出关键帧百分比；他们将按照其应该发生的顺序来处理。

```css
@keyframes slidein {
  from {
    margin-left: 100%; width: 300%;
  }
  to {
    margin-left: 0%; width: 100%;
  }
}
/* 如果一个关键帧中没有出现其他关键帧中的属性，那么这个属性将使用插值(不能使用插值的属性除外, 这些属性会被忽略掉)。例如： */
@keyframes identifier {
  0% { top: 0; left: 0; }
  30% { top: 50px; }
  68%, 72% { left: 50px; }
  100% { top: 100px; left: 100%; }
}
```



1、`<Animation Name>`的命名规范

```javascript
// 命名需要遵循以下规则
const rIsInvalid = /^--|^[0-9]+-|^(?:unset|initial|inherit|none)$/
    , rIsValid = /^[0-9a-z-_\\]+$/i
function isValidAnimationName(animationName: string): boolean{
  return !rIsInvalid.test(animationName) && rIsValid(animationName)
}
```

2、`<Animation Time Offset>`取值
`0-100%`、`from`，等价与`0%`、 `to`，等价与`100%`。
3、`<Animation Name>`重复怎么办
@keyframes CSS规则不支持层叠样式，因此当出现多个同名keyframes，那么仅最后出现的那个有效。

```css
/* 无效 */
@keyframes rotate {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}
/* 生效 */
@keyframes rotate {
  from { transform: rotate(90deg); }
  to { transform: rotate(-360deg); }
}
```

4、`<Animation Time Offset>`重复怎么办
与@keyframes CSS规则一样，标准规定相同的关键帧不产生层叠，仅最后出现的认定为有效。
但实际上FireFox14+和Chrome均将关键帧设计为可层叠的。

```css
@keyframes rotate {
  from { transform: rotate(0deg); }
  from { background: red; }
  /* 上述两条time offset实际上等价于
   * from { transform: rotate(0deg); background: red; }
   */
  to {
    transform: rotate(360deg);
    background: yellow;
  }
}
```

5、`!important`导致属性失效
一般情况下使用`!important`会让CSS属性获得最高权重，但在@keyframes下却会导致该CSS属性失效。

```less
@keyframes rotate {
  from {
    transform: rotate(90deg);
    background: red!important; /* background属性无效 */
  }
  to { transform: rotate(-360deg); }
}
```

6、必须提供至少两个关键帧

```less
/* 不会根据缓动函数产生动画效果，而是在动画持续时间的最后瞬间移动过去 */
@keyframes move-left{
   to {
       left: 100px;
   }
}
```

### 3.2 配置动画效果

创建动画序列，需要使用[`animation`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/animation)属性或其子属性，该属性允许配置动画时间、时长以及其他动画细节，但该属性不能配置动画的实际表现，动画的实际表现是由 [`@keyframes`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/@keyframes)规则实现， 

```
animation:
[animation-name] [animation-duration] // 动画的名称、持续时间
[animation-timing-function][animation-delay] // 关于时间的函数(properties/t)、延迟时间
[animation-iteration-count] [animation-direction] // 播放次数、播放顺序
[animation-fill-mode] [animation-play-state]; // 播放前或停止后设置相应样式、控制动画运行或暂停
```

示例：

```less
.box.rotate {
  animation: rotate 10s infinite alternate;
}
```









## 4. 参考资料

[深入理解CSS过渡属性transition 简书](https://www.jianshu.com/p/5dbeeb2159e8)

[CSS3属性transform详解](https://www.cnblogs.com/aspnetjia/p/5139020.html)

[CSS3（三）Animation 入门详解 CSDN](https://blog.csdn.net/u013243347/article/details/79976352)

[CSS Animations MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Animations)

[使用 CSS 动画 MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Animations/Using_CSS_animations)

[CSS3中的关键帧 MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/@keyframes)

[CSS魔法堂：更丰富的前端动效by CSS Animation 来自segmentfault](https://segmentfault.com/a/1190000015588193)

