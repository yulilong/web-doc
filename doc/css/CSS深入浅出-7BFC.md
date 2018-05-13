## CSS规范中对 BFC 的描述

http://www.ayqy.net/doc/css2-1/visuren.html#block-formatting

9.4.1 块格式化上下文

浮动，绝对定位元素，非块盒的块容器（例如，inline-blocks，table-cells和table-captions）和'overflow'不为'visible'的块盒会为它们的内容建立一个新的块格式化上下文

在一个块格式化上下文中，盒在竖直方向一个接一个地放置，从包含块的顶部开始。两个兄弟盒之间的竖直距离由'margin'属性决定。同一个块格式化上下文中的相邻块级盒之间的竖直margin会合并

在一个块格式化上下文中，每个盒的left外边（left outer edge）挨着包含块的left边（对于从右向左的格式化，right边挨着）。即使存在浮动（尽管一个盒的行盒可能会因为浮动收缩），这也成立。除非该盒建立了一个新的块格式化上下文（这种情况下，该盒自身可能会因为浮动变窄）



## MDN 对 BFC 的描述

**块格式化上下文（Block Formatting Context，BFC）** 是Web页面的可视化CSS渲染的一部分，是布局过程中生成块级盒子的区域，也是浮动元素与其他元素的交互限定区域。

下列方式会创建**块格式化上下文**：

- 根元素或包含根元素的元素
- 浮动元素（元素的 float 不是 none）
- 绝对定位元素（元素的 position 为 absolute 或 fixed）
- 行内块元素（元素的 display 为 inline-block）
- 表格单元格（元素的 display为 table-cell，HTML表格单元格默认为该值）
- 表格标题（元素的 display 为 table-caption，HTML表格标题默认为该值）
- 匿名表格单元格元素（元素的 display为 table、table-row、 table-row-group、table-header-group、table-footer-group（分别是HTML table、row、tbody、thead、tfoot的默认属性）或 inline-table）
- overflow 值不为 visible 的块元素
- display 值为 flow-root 的元素
- contain 值为 layout、content或 strict 的元素
- 弹性元素（display为 flex 或 inline-flex元素的直接子元素）
- 网格元素（display为 grid 或 inline-grid 元素的直接子元素）
- 多列容器（元素的 column-count 或 column-width 不为 auto，包括 column-count 为 1）
- column-span 为 all 的元素始终会创建一个新的BFC，即使该元素没有包裹在一个多列容器中

创建了块格式化上下文的元素中的所有内容都会被包含到该BFC中。**除了被包含于创建新的块级格式化上下文的后代元素内的元素。**

块格式化上下文对浮动定位（参见 float）与清除浮动（参见 clear）都很重要。浮动定位和清除浮动时只会应用于同一个BFC内的元素。浮动不会影响其它BFC中元素的布局，而清除浮动只能清除同一BFC中在它前面的元素的浮动。外边距折叠（Margin collapsing）也只会发生在属于同一BFC的块级元素之间。

https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Block_formatting_context



### 特别说明：`display: flow-root`

CSS最新属性， 可是使DIV标签触发BFC，而没有其他任何副作用。



## 张鑫旭对 BFC 的描述

http://www.zhangxinxu.com/wordpress/2015/02/css-deep-understand-flow-bfc-column-two-auto-layout/

BFC全称”Block Formatting Context”, 中文为“块级格式化上下文”。啪啦啪啦特性什么的，一言难尽，大家可以自行去查找，我这里不详述，免得乱了主次，总之，记住这么一句话：BFC元素特性表现原则就是，内部子元素再怎么翻江倒海，翻云覆雨都不会影响外部的元素。所以，避免margin穿透啊，清除浮动什么的也好理解了。



## BFC到底是什么？

1. 我不知道什么是 BFC
2. 但是你写出样式，我就知道这是不是 BFC

BFC 就是这样的东西（堆叠上下文也是）

1. 它没有定义
2. 它只有特性/功能

### 功能1： 爸爸管儿子：父元素包住所有子元素

用 BFC 包住浮动元素。(可以达到清除浮动的效果，但是不是清除浮动，.clearfix 才是清除浮动）

```html
<body>
  <style>
    .dad { border: 5px solid; overflow: hidden; }
    .son {
      height: 150px; width: 300px; background: red;
      float: left;
    }
  </style>
  <div class="dad">
    <div class="son"></div>
  </div>
</body>
<!-- http://js.jirengu.com/xumij/1/edit -->
```



还有：

BFC会包含所有的子元素， 如果子元素中有BFC，那么久只包含到这个子元素， 子元素BFC里面有子元素自己去管。（MDN）

```html
<body>
  <style>
    .dad { border: 5px solid; position: absolute; }
    .son {
      height: 250px; width: 400px; background: red;
      float: left; margin-top: 50px; height: 100px;
    }
    .grandson {
      height: 100px; width: 200px; margin-top: 100px; background: green;
    }
  </style>
  <div class="dad">
    <div class="son">
      <div class="grandson">11</div>
    </div>
  </div>
</body>
<!-- http://js.jirengu.com/xumij/3/edit -->
```

效果：

```
+-----------------------------------+
|                              dad  |
+---------------------------+       |
||  son                     |       |
|---------------------------+       |
|-----------------------------------+
+----------------------+
|     grandson         |
+----------------------+

```



### 功能2： 兄弟之间划清界限：两个BFC之间划清界限

BFC会和浮动元素不产生任何交集，顺着浮动边缘形成自己的封闭上下文。BFC会自动填满除去浮动内容以外的剩余空间，这就是自适应布局。

用 float + div 做左右自适应布局

```html
<body>
  <style>
    .one {
      border: 1px solid red;
      margin-right: 20px;
      width: 100px;
      height: 300px;
      float: left;
    }
    .two {
      border: 1px solid;
      height: 300px;
      overflow: hidden;
    }
  </style>
  <div class="one"></div>
  <div class="two"></div>
</body>
<!-- http://js.jirengu.com/zenem/1/edit -->
```

这里想要在两个元素有间距，在BFC中加`margin-left`需要大于100px才会生效，要么在float元素中加`margin-right`。



## 功能三： 阻止margin合并

```html
<body>
  <style>
    .dad { outline: 5px solid; overflow: hidden; }
    .son{ height: 150px; border: 5px solid red; margin-top: 100px; }
  </style>
  <div class="dad">
    <div class="son"></div>
  </div>
</body>
<!-- http://js.jirengu.com/podub/1/edit -->
```



### 如何回答面试官

1. 千万别解释什么是 BFC，一解释就错
2. 用上面的例子回答什么是 BFC

