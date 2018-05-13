## 堆叠顺序

[深入理解CSS中的层叠上下文和层叠顺序]()

“层叠顺序”英文称作”stacking order”. 表示元素发生层叠时候有着特定的垂直显示顺序，叠顺序规则:

```
显 示 器
 +-------------------+  <-----+ 装 饰
 |  background/border|
 |     +----------------------+
 |     |   负 z-index         |
 +-----+    +-----------------------+
       |    |   div/块 级 元 素      |   <---+ 布 局
       |    |  +-----------------------+
       +----+  |  float浮 动 元 素      |
            |  | +-----------------------+
            +--+ |inline/inline-block盒子 | <--+ 内 容
               +-+  +------------------------+
                 |  | z-index:0/z-index:auto |
                 +--+ +------------------------+
                    +-+  正 z-index            |
                      +------------------------+

                                          用 户 眼 睛
```

从用户的眼睛到显示之间堆叠的顺序依次：

1. 正z-index
2. z-index:0/z-index:auto(position:relative)
3. inline/inline-block元素
4. float浮动元素
5. 块级元素
6. 负z-index
7. border
8. background



### 1、`border`在`background`上的例子

当边框的颜色设置透明度时，背景色改变，视觉上边框的颜色也变了，说明`border`在`background`上。

```html
<style>
    div {
      border: 10px solid rgba(255,0,0, 0.2);
      width: 300px; height: 200px;
      background: green;
	/*background: yellow; */
    }
</style>
<div></div>
```

### 2、说明div块元素在`border`上的例子

可以看见子div把父div的`border`覆盖了。

```html
<style>
    .dad {
      border: 10px solid rgba(255,0,0, 1);
      width: 300px; height: 200px; background: green;
    }
    .son {
      width: 70px; height: 20px;
      background: blue; color: black;
      margin-left: -5px;
    }
</style>
<div class="dad">
    父元素
    <div class="son"></div>
</div>
```

父div中内联元素与字div中内联元素发生堆叠，后面覆盖前面的

下面的例子中，父div中内联元素由于在子div中内联元素的前面，所以被覆盖了， 同级的元素也是后面的覆盖前面的。

```html
<style>
    .dad {
      border: 10px solid rgba(255,0,0, 1);
      width: 300px; height: 200px;
      background: green; color: red;
    }
    .son {
      width: 70px; height: 20px;
      background: blue; color: black;
      margin-top: -10px;
    }
    .son1 {
      color: yellow; margin-bottom: -10px;
    }
  </style>
<div class="dad">
    父元素
    <div class="son"> 子元素 </div>
    <div class="son1 son">子元素</div>
    父元素
</div>
```



### 3、说明float浮动元素在div上的例子

在这个例子中，浮动元素覆盖了div元素。

```html
<style>
    .dad {
      border: 10px solid rgba(255,0,0, 1);
      width: 300px; height: 200px; background: green;
      text-indent: -10px;
    }
    .son {
      width: 70px; height: 20px;
      background: yellow; color: black;
      margin-left: -5px;
    }
    .float {
      width: 50px; height: 50px; background: blue;
      float: left;
    }
  </style>
<div class="dad">
    父元素
    <div class="float"></div>
    <div class="son"></div>
</div>
```



### 4、说明内联元素在float浮动元素上面的例子

可以看见内联元素在浮动元素的上面。 

内联元素也比浮动元素中的内联元素靠前（在前面）。

浮动元素中的内联元素优先级是没有外边的内联元素优先级高。

```html
<style>
    .dad {
      border: 10px solid rgba(255,0,0, 1);
      width: 300px; height: 200px; background: green;
      text-indent: -20px;
    }
    .float {
      width: 50px; height: 50px; background: blue;
      float: left; color: red;
    }
</style>
<div class="dad">
    父元素
    <div class="float">浮动元素</div>
</div>
```

### 5、`z-index`的值大于等于0的元素在内联元素的上面

`z-index`的值是`auto`相当于0。

`z-index`属性只能给`position`的值是`relative`、`absolute`、`fixed`设置才会生效。

在下面的例子中，`z-index`的值大于等于0的元素覆盖在内联元素上面。

而`z-index`的值大的覆盖小的。

```html
<style>
    .dad {
      border: 10px solid rgba(255,0,0, 1);
      width: 300px; height: 200px; background: #ccc;
    }
    .float {
      width: 50px; height: 150px; background: blue;
      float: left; color: red;
    }
    .relative {
      width: 150px; height: 20px;background: yellow;
      position: relative;
      margin-top: -10px;
    }
    .absolute {
      width: 50px; height: 60px;background: green;
      position: absolute; margin-top: -10px;
      z-index: 1;
    }
    .rel {z-index: 1; margin-top: 0;background: white}
</style>
<div class="dad">
    11
    <div class="float"></div>
    <div class="relative"></div>
    <div class="absolute"></div>
    <div class="relative rel"></div>
</div>
```



### 6、`z-index`的值为负数的元素在`background`的后面



```html
<style>
    .dad {
      border: 10px solid red; width: 300px; height: 100px; background: #ccc;
    }
    .negative {
      width: 50px; height: 150px;background: green;
      position: absolute;
      z-index: -1;
    }
</style>
<div class="dad">
    <div class="negative"></div>
</div>
```



## 层叠上下文(堆叠上下文)

[mdn层叠上下文介绍](https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Understanding_z_index/The_stacking_context)

层叠上下文是HTML元素的三维概念，这些HTML元素在一条假想的相对于面向（电脑屏幕的）视窗或者网页的用户的z轴上延伸，HTML元素依据其自身属性按照优先级顺序占用层叠上下文的空间。



满足下面任何一个条件就会触发层叠上下文：

- 根元素 (HTML),
- z-index 值不为 "auto"的 绝对/相对定位，
- position: fixed
- 一个 z-index 值不为 "auto"的 flex 项目 (flex item)，即：父元素 display: flex|inline-flex，
- opacity 属性值小于 1 的元素（参考 the specification for opacity），
- transform 属性值不为 "none"的元素，
- mix-blend-mode 属性值不为 "normal"的元素，
- filter值不为“none”的元素，
- perspective值不为“none”的元素，
- isolation 属性被设置为 "isolate"的元素，
- 在 will-change 中指定了任意 CSS 属性，即便你没有直接指定这些属性的值（参考 这篇文章）
- -webkit-overflow-scrolling 属性被设置 "touch"的元素

层叠上下文主要影响`z-index`的属性。



从上面的条件中可以看见，一个网页会有一个默认的层叠上下文(根元素 HTML),当元素发生堆叠的时候：

1. 从元素往上找，找到父辈中触发了层叠上下文的元素，没有就是根元素。
2. 两个父辈触发层叠上下文的元素比较堆叠优先级，高的子元素在上面。
3. 如果父辈元素堆叠优先级相同，后面的覆盖前面的。
4. 如果他们的触发层叠上下文的父辈元素时同一个，那么就按照层叠顺序堆叠。



在下面的例子中：

1. 父元素的层叠上下文优先级相同时，那么b1覆盖a1，
2. 把a元素的层叠上下文优先级变大，那么b1则在整个a元素下面。
3. 如果a元素和b元素同时修改为`z-index:zuto`，那么a1元素在b1元素上面。



```html
<style>
    /*http://js.jirengu.com/fogij/8/edit*/
    .dad { width: 300px; height: 200px; background: #ccc; }
    .negative {
      width: 150px; height: 70px;background: green;
      position: relative;
    }
    .a1,.b1 {
       width: 100px; height: 20px;background: yellow;
       position: relative;
    }
    .a1 {z-index: 10;}
    .b1 {background: blue; margin-top: -55px; z-index: 0;}
    .a { z-index: 2; }
    .b { z-index: 2; width: 170px; background: white;}
</style>
<div class="dad">
    <div class="negative a">a
        <div class="a1">a1</div>
    </div>
    <div class="negative b">b
        <div class="b1">b1</div>
    </div>
</div>
```

