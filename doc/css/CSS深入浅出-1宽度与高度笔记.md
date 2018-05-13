## chrome开发者工具查看一个HTML元素具体属性

如果想要知道页面上一个HTML元素的摸个属性值：

1. 在chrome浏览器中，右键 -> 检查,打开开发者工具。
2. 点一下左上角的'Select an elements …'按钮，然后选择需要查看的HTML元素。
3. 开发者工具中右边选择： Computed, 在下面的输入框中选择需要的查看的属性。

![](http://p1ibqa9uh.bkt.clouddn.com/18-3-27/75427682.jpg)



## 字体  



1. 字与字之间是通过基线对其的
2. 字体设计师会把建议行高写在字体文件里（如：1.2倍字体大小），可使用line-height明确设置行高，
3. 不同字体空格的宽度是不一样的。



## 块元素高度

1. 如果div元素里面只有一行内联元素： div高度就是这个内联元素的行高，内联元素的行高由字体的建议行高确定，如果设置了`line-height`，则由`line-height`确定.

2. div元素里有多行内联元素： 由多行内联元素的行高相加确定。

3. div里面有div，那么div高度：子div高度 + 子div padding + 子div border (如果有阻挡那么再+ 子div margin)

   ​

   `outline`属性跟`border`属性一样，区别是`outline`属性不占用空间。




**总结：** div的高度是由div内部文档流中元素的高度的总和决定的，不计算脱离文档流的高度。



## 脱离文档流

脱离文档流就是再计算div高度的时候，不要算上脱离的元素。

可脱离文档流的属性：`float:left``position:absolute``position:fixed`,相对定位没有脱离文档流，还可以定位，还可以相对于自己的位置定位。


## HTML文本两端对齐（套路一）

```html
<style>
    div { border: 1px solid }
    span {
      display: inline-block;
      border: 1px solid;
      width: 5em;
      text-align: justify;
      line-height: 25px;
      height: 25px;
      overflow: hidden;
    }
    span::after {
      content: '';
      display: inline-block;
      width: 100%;
      border: 1px solid blue;
    }
  </style>
<div>
    <span>姓名</span> <br>
    <span>联系方式</span>
</div>
```



## HTML特性： 自动删除、合并多余空格

HTML会把所有内联元素之外的空格删除， 内联元素之间所有看不见的字符合并成一个空格。

```html
<!--会有空格:1 2 -->
<span>1</span>
<span>2</span>
```

不管是`inline`还是`inline-block`元素， 只要两个元素之间有：回车、table、空格等任何看不见的字符，就会有空格。这个是HTML机制，不是bug。

内联元素不可以设置宽高。



## 响应式页面、文档流

响应式： 随着页面大小变化，页面内容也跟着变化而自动排版，叫响应式页面。

文档流： 如果内联元素足够多，一行排列不下，那么就会自动换行，叫文档流。内联元素从左到右排列，块级元素从上到下排列， 每一个块都会另起一行，即使一行可以容纳2个块元素，这两个块元素也不会在一行。



## 单词太长一行放不下

正常来说没有那么长的单词

如果单词太长：

1. 使用单词连字符`-`，使用连字符浏览器就知道在哪里该换行。

   ```html
   <style>
       div { width: 100px; border: 1px solid; }
   </style>
   <div>helllllllllllllllllll-llllo</div>
   ```

2. 使用`word-break:break-all` （单词的中断：中断所有）单词哪里都可以换行，文档流相关

   ```
   <style>
       div { width: 100px; border: 1px solid; word-break: break-all;}
   </style>
   <div>helllllllllllllllllll-llllo</div>
   ```

## 单行文字溢出省略

div的宽度不是由文字决定的。

```html
<style>
    div {
      width: 100px;
      border: 1px solid;
      white-space: nowrap;		// 规定段落中的文本不进行换行
      overflow: hidden;		
      text-overflow: ellipsis; // 显示省略符号来代表被修剪的文本
    }
  </style>
<div>13213213131232132132132131</div>
```



## 多行文本溢出省略

可在Google上搜索：`css multi line text ellipsis`

https://css-tricks.com/line-clampin/

```html
<style>
    div {
      width: 100px;
      border: 1px solid;
      display: -webkit-box;
      -webkit-line-clamp: 3;	// 显示三行，超过三行溢出省略，
      -webkit-box-orient: vertical;  
      overflow: hidden;
    }
  </style>
<div>13213213-13-12321-32-1321-32-131d-sadadsad</div>
```

上面是只能在`-webkit`中生效。 不兼容IE浏览器，手机浏览器也支持这种效果。电脑端： chrome、opera、Safari都支持。只有IE和火狐不支持。火狐用的人很少，

可以查看浏览器使用统计(百度统计 浏览器):

http://tongji.baidu.com/data/browser    



## 文本垂直居中(父元素是div,子元素是内联元素)

1. 规定了高度（40px）

   不要使用`height: 40px;line-height: 40px;` 这个样式如果是一行没问题，多行文本那么就会出现bug。

   推荐用法：`line-height:24px; padding: 8px 0;`,这样的好处是不管是一行文本还是多行文本，都不会出现bug。

   对于规定了高度，尽量不使用`height：40xp;`.可使用`line-height`加`padding`的做法凑到40px。

   *注意*：` border`属性实会占据空间，如果不想占用空间可使用`outline`属性。

   ```html
   <style>
       div {
         width: 100px;
         outline: 1px solid;
         line-height: 24px;
         padding: 8px 0;		// 垂直居中： line-height和padding 
         text-align: center;	// 水平居中
       }
     </style>
   <div>132132</div>
   ```



## div里面的div垂直水平居中

尽量不要用`height`。

1. 仅仅是垂直居中：

   垂直居中：可在父元素中设置`padding：50px 0;`,

   水平居中：可在子元素中设置`margin: 0 auto;`

   ```html
   <style>
       .father {
           border: 1px solid red; padding: 50px 0;
       }
       .son  {
           border: 1px solid green; width: 100px; margin: 0 auto; 
       }
   </style>
   <div class="father">
     <div class="son">12345132 1dd dd</div>
   </div>
   ```

2. 父元素高度固定，子元素高度固定，宽度固定

   垂直、水平居中：子元素绝对定位，距离上下左右都是0，然后设置`margin: auto`

   ```html
   <style>
   	.father {
           border: 1px solid red; height: 200px; position: relative;
       }
       .son  {
           border: 1px solid green;  width: 100px; height: 100px;
           position: absolute; top: 0; bottom: 0; left: 0; right: 0;
           margin: auto;
       }
   </style>
   <div class="father">
     	<div class="son">12345132 1dd dd</div>
   </div>
   ```

3. 父元素高度固定，子元素高度不确定

   使用`flex`布局，

   不兼容IE浏览器。

   ```html
   <style>
       .father {
           border: 1px solid red; height: 200px;
           display: flex;
           justify-content: center;// 水平居中：定义flex子项在flex容器的当前行水平方向对齐方式
           align-items: center;	// 垂直居中：定义flex子项在flex容器的当前行垂直方向对齐方式
       }
       .son  {
           border: 1px solid green;  width: 100px;
       }
   </style>
   <div class="father">
     	<div class="son">12345132 1dd dd</div>
   </div>
   ```

   ​

## margin合并(仅垂直方向合并，水平方向不合并)

父子元素的margin合并：

如果没有阻挡，那么父子元素的上下margin就会产生合并。左右margin没有合并。

阻止合并的方法：在父元素中设置`padding`或设置`border`或设置`overflow:hidden`,父子之间有内联元素，也会阻止margin合并

## 总结

1. 内联元素的宽高：

   宽度由内联元素的中字的个数确定，`padding`、`margin`、`border`会影响宽度

   高度：由行高决定的。`padding`、`margin`、`border`不影响高度

2. 块元素的宽高：

   宽度： 自适应。默认继承父元素的宽度。

   高度：div的高度是由div内部文档流中元素的高度的总和决定的，不计算脱离文档流的高度。

3. 文档流： 布局从左到有，从上到下。

4. 实现一个一比一的div

   高度是0， 设置`padding-top: 100%`的意思是跟宽度一样。

   ```html
   <style>
       .one {  
           border: 1px solid; 
           padding-top: 100%;	// padding-top 100% 跟宽度一样
       }
   </style>
   <div class="one"></div>
   ```

   ​