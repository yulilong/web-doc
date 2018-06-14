[TOC]

## 1. 选择器类型

1. 基础选择器
2. 组合选择器
3. 属性选择器
4. 伪类选择器
5. 伪元素选择器

## 2. 基础选择器

选择器   | 含义
:--  | :--
\*    | 通用元素选择器，匹配页面任何元素（这也就决定了我们很少使用）
\#id  | id选择器，匹配特定id的元素
.class  | 类选择器，匹配class**包含**(不是等于)特定类的元素
element | 标签选择器

### 2.1 范例
```
  * {
    margin: 0;
    padding: 0;
    }

  #id-selector{
    color: #333;
  }

  .class-selector{
    background: #ccc;
  }

  p {
    font-size: 20px;
  }
```


## 3. 组合选择器

选择器     | 含义
:--      | :--
E,F       | 多元素选择器，用`,`分隔，同时匹配元素E或元素F
E F       | 后代选择器，用空格分隔，匹配E元素所有的**后代**（不只是子元素、子元素向下递归）元素F
E>F       | 子元素选择器，用`>`分隔，匹配E元素的所有**直接子元素**
E+F       | 直接相邻选择器，匹配E元素之后的相邻的同级元素F
E~F       | 普通相邻选择器（弟弟选择器），匹配E元素之后的同级元素F（无论直接相邻与否）
.class1.class2  | id和class选择器和选择器连写的时候中间没有分隔符，`.` 和 `#` 本身充当分隔符的元素
element#id    | id和class选择器和选择器连写的时候中间没有分隔符，`.` 和 `#` 本身充当分隔符的元素

## 4. 属性选择器

选择器         | 含义
--           | --
E[attr]         | 匹配所有具有属性attr的元素，div[id]就能取到所有有id属性的div
E[attr = value]     | 匹配属性attr值为value的元素，div[id=test],匹配id=test的div
E[attr ~= value]    | 匹配所有属性attr具有多个空格分隔、其中一个值等于value的元素
E[attr ^= value]    | 匹配属性attr的值以value**开头**的元素
E[attr $= value]    | 匹配属性attr的值以value**结尾**的元素
E[attr *= value]    | 匹配属性attr的值**包含**value的元素

## 5. 伪类选择器

选择器         | 含义
--           | --
E:first-child     | 匹配作为长子（第一个子女）的元素E
E:link          | 匹配所有未被点击的链接
E:visited       | 匹配所有已被点击的链接
E:active        | 匹配鼠标已经其上按下、还没有释放的E元素
E:hover         | 匹配鼠标悬停其上的E元素
E:focus         | 匹配获得当前焦点的E元素
E:lang(c)       | 匹配lang属性等于c的E元素
E:enabled       | 匹配表单中可用的元素
E:disabled        | 匹配表单中禁用的元素
E:checked       | 匹配表单中被选中的radio或checkbox元素
E::selection      | 匹配用户当前选中的元素

所有选择器列表在 [MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Reference#选择器)

## 6. 伪类选择器

选择器         | 含义
--           | --
E:root          | 匹配文档的根元素，对于HTML文档，就是HTML元素
E:nth-child(n)      | 匹配其父元素的第n个子元素，第一个编号为1
E:nth-last-child(n)   | 匹配其父元素的倒数第n个子元素，第一个编号为1
E:nth-of-type(n)    | 与:nth-child()作用类似，但是仅匹配使用同种标签的元素
E:nth-last-of-type(n) | 与:nth-last-child() 作用类似，但是仅匹配使用同种标签的元素
E:last-child      | 匹配父元素的最后一个子元素，等同于:nth-last-child(1)
E:first-of-type     | 匹配父元素下使用同种标签的第一个子元素，等同于:nth-of-type(1)
E:last-of-type      | 匹配父元素下使用同种标签的最后一个子元素，等同于:nth-last-of-type(1)
E:only-child      | 匹配父元素下仅有的一个子元素，等同于:first-child:last-child或 :nth-child(1):nth-last-child(1)
E:only-of-type      | 匹配父元素下使用同种标签的唯一一个子元素，等同于:first-of-type:last-of-type或 :nth-of-type(1):nth-last-of-type(1)
E:empty         | 匹配一个不包含任何子元素的元素，文本节点也被看作子元素
E:not(selector)     | 匹配不符合当前选择器的任何元素

### 6.1 n的取值

* 1，2，3，4，5
* 2n+1, 2n, 4n-1
* odd, even


## 7. 伪元素选择器

选择器     | 含义
--       | --
E::first-line | 匹配E元素内容的第一行
E::first-letter | 匹配E元素内容的第一个字母
E::before   | 在E元素之前插入生成的内容
E::after      | 在E元素之后插入生成的内容

## 8. 选择器优先级

如果多条规则作用于同一个元素上，且定义的相同属性的不同值，比如
```
  <style>
    #test {color: #666;}
    p {color: #333;}
  </style>

  <p id="text">Text</p>
```
这种场景下，`p`元素文本颜色应该是哪个呢？


## 9. CSS优先级

**从高到低分别是**

1. 在属性后面使用 `!important` 会覆盖页面内任何位置定义的元素样式
2. 作为style属性写在元素标签上的内联样式
3. id选择器
4. 类选择器
5. 伪类选择器
6. 属性选择器
7. 标签选择器
8. 通配符选择器
9. 浏览器自定义

### 9.1 复杂场景
```
  #test p.class1 {...}
  #test .class1.class2 {...}
```

- 行内样式 `<div style="xxx"></div>` ==> a
- ID 选择器  ==> b
- 类，属性选择器和伪类选择器 ==> c
- 标签选择器、伪元素 ==> d

### 9.2 小测试

```
*             {}  /* a=0 b=0 c=0 d=0 -> 0,0,0,0 */
p             {}  /* a=0 b=0 c=0 d=1 -> 0,0,0,1 */
a:hover       {}  /* a=0 b=0 c=1 d=1 -> 0,0,1,1 */
ul li         {}  /* a=0 b=0 c=0 d=2 -> 0,0,0,2 */
ul ol+li      {}  /* a=0 b=0 c=0 d=3 -> 0,0,0,3 */
h1+input[type=hidden]{}  /* a=0 b=0 c=1 d=2 -> 0,0,1,2 */
ul ol li.active   {}  /* a=0 b=0 c=1 d=3 -> 0,0,1,3 */
#ct .box p        {}  /* a=0 b=1 c=1 d=1 -> 0,1,1,1 */
div#header:after  {}  /* a=0 b=1 c=0 d=2 -> 0,1,0,2 */
style=""          /* a=1 b=0 c=0 d=0 -> 1,0,0,0 */

```


### 9.3 样式覆盖
```
  div {color: #333;}
  ....
  div {color: #666;}
```

这样`div`文案的颜色明显会是`#666`

##  10. 选择器使用经验
- 遵守 CSS 书写规范
- 使用合适的命名空间
- 合理的复用class

<style>
  table{
    font-size: .8em!important;
  }
</style>
