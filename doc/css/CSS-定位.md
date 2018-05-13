
## 基本属性


值     | 属性
:---    | :---
inherit   | 规定应该从父元素继承 position 属性的值
static    | 默认值,没有定位，元素出现在正常的流中（忽略 top, bottom, left, right 或者 z-index 声明）
relative  | 生成相对定位的元素，相对于元素本身正常位置进行定位,因此，`left:20px` 会向元素的 left 位置添加20px
absolute  | 生成绝对定位的元素，相对于`static`定位以外的第一个祖先元素（offset parent）进行定位,元素的位置通过 `left`, `top`, `right` 以及 `bottom` 属性进行规定
fixed   | 生成绝对定位的元素，相对于浏览器窗口进行定位。元素的位置通过 `left`, `top`, `right` 以及 `bottom` 属性进行规定
sticky    | CSS3新属性，表现类似`position:relative`和`position:fixed`的合体，在目标区域在屏幕中可见时，它的行为就像position:relative; 而当页面滚动超出目标区域时，它的表现就像position:fixed，它会固定在目标位置

绝对定位、固定定位 如果不设置`left`, `top`, `right` 以及 `bottom`时，元素位置还是在原来的位置，当设置`left`, `top`, `right` 以及 `bottom`时，距离的是最近上级元素是`relative`、`absolute`、`fixed`、`sticky`。    


##  定位机制

CSS有三种基本的定位机制：普通流，浮动，绝对定位(absolute,fixed)


- 普通流是默认定位方式，在普通流中元素框的位置由元素在html中的位置决定，这也是我们最常见的方式，其中`position: static`与`position:relative`属于普通流的定位方式
- 浮动定位定位机制后续讲解
- 绝对定位包括 absolute和 fixed



## Position 的几个值

**static**
```
  <div style="border: solid 1px #0e0; width:200px; position: static;">
      <div style="height: 100px; width: 100px; background-color: Red;">
      </div>
      <div style="height: 100px; width: 100px; background-color: Green;">
      </div>
      <div style="height: 100px; width: 100px; background-color: Red;">
      </div>
  </div>
```
<div style="border: solid 1px #0e0; width:200px; position: static;">
    <div style="height: 100px; width: 100px; background-color: Red;">
    </div>
    <div style="height: 100px; width: 100px; background-color: Green;">
    </div>
    <div style="height: 100px; width: 100px; background-color: Red;">
    </div>
</div>

###
**relative**
```
  <div style="border: solid 1px #0e0; width:200px;">
      <div style="height: 100px; width: 100px; background-color: Red;">
      </div>
      <div style="height: 100px; width: 100px; background-color: Green; position:relative; top:20px; left:20px;">
      </div>
      <div style="height: 100px; width: 100px; background-color: Red;">
      </div>
  </div>
```
<div style="border: solid 1px #0e0; width:200px;">
    <div style="height: 100px; width: 100px; background-color: Red;">
    </div>
    <div style="height: 100px; width: 100px; background-color: Green; position:relative; top:20px; left:20px;">
    </div>
    <div style="height: 100px; width: 100px; background-color: Red;">
    </div>
</div>


## absolute 和 fixed

- 相对定位可以看作特殊的普通流定位，元素位置是相对于它在普通流中位置发生变化，而绝对定位使元素的位置与文档流无关，也不占据文档流空间，普通流中的元素布局就像绝对定位元素不存在一样

- 绝对定位的元素的位置是相对于距离最近的`非static祖先元素`位置决定的。如果元素没有已定位的祖先元素，那么他的位置就相对于初始包含块html来定位[demo](http://js.jirengu.com/jeko)。

- 因为绝对定位与文档流无关，所以绝对定位的元素可以覆盖页面上的其他元素，可以通过`z-index`属性控制叠放顺序，z-index越高，元素位置越靠上。


###
```

  <div style="border: solid 1px #0e0; width:200px; position:relative;">
      <div style="height: 100px; width: 100px; background-color: Red;">
      </div>
      <div style="height: 100px; width: 100px; background-color: Green; position:absolute; top:20px; left:20px;">
      </div>
      <div style="height: 100px; width: 100px; background-color: Yellow;">
      </div>
  </div>
```
<div style="border: solid 1px #0e0; width:200px; position:relative;">
    <div style="height: 100px; width: 100px; background-color: Red;">
    </div>
    <div style="height: 100px; width: 100px; background-color: Green; position:absolute; top:20px; left:20px;">
    </div>
    <div style="height: 100px; width: 100px; background-color: Yellow;">
    </div>
</div>

### 

fixed固定定位，固定定位是绝对定位的一种，固定定位的元素也不包含在普通文档流中，差异是固定元素的包含块儿是视口（viewport）
```
  <div style="border: solid 1px #0e0; width:200px;">
      <div style="height: 100px; width: 100px; background-color: Red;">
      </div>
      <div style="height: 100px; width: 100px; background-color: Green; position:fixed; bottom:20px; left:20px;">
      </div>
      <div style="height: 100px; width: 100px; background-color: Yellow;">
      </div>
  </div>
```
<div style="border: solid 1px #0e0; width:200px;">
    <div style="height: 100px; width: 100px; background-color: Red;">
    </div>
    <div style="height: 100px; width: 100px; background-color: Green; position:fixed; bottom:20px; left:20px;">
    </div>
    <div style="height: 100px; width: 100px; background-color: Yellow;">
    </div>
</div>


## 绝对定位宽度
> 绝对定位宽度是收缩的，如果想撑满父容器，可以设置 `width: 100%`
```
<div style="position: absolute; background: red">
hello 饥人谷
</div>
```
<div style="position: absolute; background: red">
hello 饥人谷
</div>

## 绝对定位和 BFC
> 绝对定位能形成 BFC
> 可用来清除浮动
> 可用来阻止外边距合并

## 行内元素加绝对定位后会达到块级特性

Span等行内元素加绝对定位后 就会达到块级特性，可以设置高度，margin上下可以设置了。 这个不是BFC。    
```
<!-- HTML代码： -->
  <div class="box3">
    <span>hello</span>
  </div>

/* CSS代码 */
.box3 {
  width: 150px;
  height: 150px;
  border: 1px solid blue;
  position: relative;
}

.box3 span {
  /* position: absolute; */
  float: left;
  width: 100px;
  height: 100px;
  margin: 10px;
  padding: 10px;
  background: green;
}
```

## 定位的应用场景

### relative   

1.自己位置的微调， 2，为子元素绝对定位设置。

等待完善。

## 绝对定位垂直水平居中

HTML代码：   
```
<body>
  <h1>hello jirengu</h1>
  <div class="container">
    <div class="box">1</div>
    <div class="box">2</div>
    <div class="box">3</div>
  </div>
</body>
```  

CSS代码：  
```
.container {
  border: 1px solid;
  position: relative;
}
.box {
  width: 100px;
  height: 100px;
  background: red;
}


/*方法一：*/
.box:nth-child(2){
  position: absolute;
  left: 50%;
  top: 50%;
  margin-left: -50px;
  margin-top: -50px;
  background: rgba(0,0,255,0.6);
}

/*方法二：*/ 
.box:nth-child(2){
  position: absolute;
  left: calc(50% - 50px);
  top: calc(50% - 50px);
  background: rgba(0,0,255,0.6);
}

/*方法三：*/ 
.box:nth-child(2){
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%); /*相对于自己偏移*/
  background: rgba(0,0,255,0.6);
  width: auto;
  height: auto;
}
```  

## 使用绝对定位、伪标签`::after`在标签右上角做一个气泡效果   

```
<!-- HTML代码： -->
<a href="#" class="btn bubble">点我</a>   

/* CSS代码 */
.btn {
  position: relative;
  text-decoration: none;
  border: 1px solid #ccc;
  display: inline-block;
  padding: 5px 10px;
  background-color: #ccc;
  color: #fff;
}
.btn.bubble::after {
  content: '';
  position: absolute;
  top: -10px;
  right: -10px;
  width: 16px;
  height: 16px;
  background: red;
  border-radius: 50%;
}
```


**2018-01-18晚上直播的定位讲解。**