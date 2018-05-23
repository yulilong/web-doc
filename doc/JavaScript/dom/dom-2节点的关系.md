[TOC]

## 描述

DOM可以将任何HTML描绘成一个由多层节点构成的结构。每个节点都拥有各自的特点、数据和方法，也与其他节点存在某种关系。节点之间的关系构成了层次，而所有页面标记则表现为一个以特定节点为根节点的树形结构。本文将详细描述DOM间的节点关系



```

             
     firstChild                 lastChild
    +------------+  +----------+ ------------------------->
    |               |  Node    |                          |
    | +---------->  |          | <----------------------+ |
    | |             +----------+ parentNode             | |
    | |parentNode            ^                          | |
    | |                      |                          | |
    | |                      |                          | |
    | |                      |parentNode                | |
    | |                      |                          | v
    v                                                   
+---+-+---+ nextSibling     ++-------+ nextSibling     ++--------+
| Node    + ------------->  | Node   |  ------------>  | Node    |
|         | <-------------+ |        | <-------------  |         |
+---------+ previousSibling +--------+ previousSibling +---------+
```

![](https://images2015.cnblogs.com/blog/740839/201608/740839-20160818204024406-666944889.jpg)

## 2. 属性

### 2.1 父级属性

#### 2.1.1 parentNode

parentNode是指定节点的父节点.一个元素节点的父节点可能是一个元素(`Element` )节点,也可能是一个文档(`Document` )节点,或者是个文档碎片(`DocumentFragment`)节点.

对于下面的[节点类型](https://developer.mozilla.org/zh-cn/DOM/Node.nodeType): Attr, Document, DocumentFragment, Entity, Notation,其parentNode属性返回null.

如果当前节点刚刚被建立,还没有被插入到DOM树中,则该节点的parentNode属性也返回null.

```html
<div id="myDiv"></div>
<script>
    console.log(myDiv.parentNode);// body
    console.log(document.body.parentNode);//html
    console.log(document.documentElement.parentNode);// #document
    console.log(document.parentNode);//null
    
    var myDiv = document.getElementById('myDiv');
    console.log(myDiv.parentNode);//body
    var fragment = document.createDocumentFragment();
    fragment.appendChild(myDiv);
    console.log(myDiv.parentNode);//document-fragment
</script>
```

[Node.parentNode](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/parentNode)

#### 2.1.2 parentElement

返回当前节点的父元素节点,如果该元素没有父节点,或者父节点不是一个元素节点.则 返回`null`.

```html
<div id="myDiv"></div>
<script>
    console.log(myDiv.parentElement);//body
    console.log(document.body.parentElement);//html
    console.log(document.documentElement.parentElement);//null
    console.log(document.parentElement);//null
</script>
```

 [注意]在IE浏览器中，只有Element元素节点才有该属性，其他浏览器则是所有类型的节点都有该属性

```html
<div id="test">123</div>
<script>
    //IE浏览器返回undefined，其他浏览器返回<div id="test">123</div>
    console.log(test.firstChild.parentElement);
    //所有浏览器都返回<body>
    console.log(test.parentElement);
</script>
```

### 2.2 子级属性

#### 2.2.1 childNodes

childNodes是一个只读的类数组对象[NodeList对象](http://www.cnblogs.com/xiaohuochai/p/5827389.html#anchor1)，它保存着该节点的第一层子节点,该集合为即时更新的集合

```html
<ul id="myUl"><li><div></div></li></ul>
<script>
    var myUl = document.getElementById('myUl');
    //结果是只包含一个li元素的类数组对象[li]
    console.log(myUl.childNodes);	// NodeList [li]
</script>
```

[Node.childNodes MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/childNodes)

#### 2.2.2 children

children是一个只读的类数组对象[HTMLCollection对象](http://www.cnblogs.com/xiaohuochai/p/5827389.html#anchor2)，但它保存的是该节点的第一层元素子节点

```html
<div id="myDiv">123</div>
<script>
    var myDiv = document.getElementById('myDiv');
    //childNodes包含所有类型的节点，所以输出[text]
    console.log(myDiv.childNodes);
    //children只包含元素节点，所以输出[]
    console.log(myDiv.children);
</script>
```

#### 2.2.3 childElementCount:返回子元素节点的个数，相当于children.length

返回子元素节点的个数，相当于children.length

[注意]IE8-浏览器不支持

```html
<ul id="myUl">
    <li></li>
    <li></li>
</ul>
<script>
var myUl = document.getElementById('myUl');
console.log(myUl.childNodes.length);//5，IE8-浏览器返回2，因为不包括空文本节点
console.log(myUl.children.length);//2
console.log(myUl.childElementCount);//2，IE8-浏览器返回undefined
</script>
```

#### 2.2.4 firstChild:第一个子节点

#### 2.2.5 lastChild:最后一个子节点

#### 2.2.6 firstElementChild:第一个元素子节点

#### 2.2.7 lastElementChild:最后一个元素子节点

上面四个属性，IE8-浏览器和标准浏览器的表现并不一致。IE8-浏览器不考虑空白文本节点，且不支持firstElementChild和lastElementChild

```html
<!-- ul标签和li标签之间有两个空白文本节点，所以按照标准来说，ul的子节点包括[空白文本节点、li元素节点、空白文本节点]。但在IE8-浏览器中，ul的子节点只包括[li元素节点] -->
<ul>
    <li></li>
</ul>
```

```html
<ul id="list">
    <li>1</li>
    <li>2</li>
    <li>3</li>
</ul>
<script>
console.log(list.firstChild); // 标准浏览器中返回空白文本节点，IE8-浏览器中返回<li>1</li>
console.log(list.lastChild);// 标准浏览器中返回空白文本节点，IE8-浏览器中返回<li>3</li> 
console.log(list.firstElementChild);// 标准浏览器中<li>1</li>，IE8-浏览器中返回undefined
console.log(list.lastElementChild);// 标准浏览器中<li>3</li>，IE8-浏览器中返回undefined 
</script>
```



### 2.3 同级属性

#### 2.3.1 nextSibling：后一个节点

#### 2.3.2 previousSibling：前一个节点

#### 2.3.3 nextElementSibling：后一个元素节点

#### 2.3.4 previousElementSibling：前一个元素节点

与子级属性类似，上面四个属性，IE8-浏览器和标准浏览器的表现并不一致。IE8-浏览器不考虑空白文本节点，且不支持nextElementSibling和previousElementSibling

```html
<ul>
    <li>1</li>
    <li id="myLi">2</li>
    <li>3</li>
</ul>
<script>
    var myLi = document.getElementById('myLi');
    console.log(myLi.nextSibling);//空白节点，IE8-浏览器返回<li>3</li>
    console.log(myLi.nextElementSibling);//<li>3</li>，IE8-浏览器返回undefined
    console.log(myLi.previousSibling);//空白节点，IE8-浏览器返回<li>1</li>
    console.log(myLi.previousElementSibling);//<li>1</li>，IE8-浏览器返回undefined
</script>
```



## 3. 方法

### 3.1 包含方法

#### 3.1.1 hasChildNodes()

hasChildNodes()方法在包含一个或多个子节点时返回true，比查询childNodes列表的length属性更简单

```html
<div id="one">123</div>
<div id="two"></div>
<script>
    var one = document.getElementById('one');
    console.log(one.childNodes.length);//1
    console.log(one.hasChildNodes());//true
    var two = document.getElementById('two');
    console.log(two.childNodes.length);//0
    console.log(two.hasChildNodes());//false
</script>
```

#### 3.1.2 contains()

contains方法接受一个节点作为参数，返回一个布尔值，表示参数节点是否为当前节点的后代节点。参数为后代节点即可，不一定是第一层子节点　

```html
<div id="myDiv">
    <ul id="myUl">
        <li id="myLi"></li>
        <li></li>
    </ul>
</div>
<script>
    console.log(myDiv.contains(myLi));//true
    console.log(myDiv.contains(myUl));//true
    console.log(myDiv.contains(myDiv));//true
</script>
```

[注意]IE和safari不支持document.contains()方法，只支持元素节点的contains()方法

```javascript
// IE和safari报错，其他浏览器返回true
console.log(document.contains(document.body));
```

### 3.2 关系方法

#### 3.2.1 compareDocumentPosition()

compareDocumentPosition方法用于确定节点间的关系，返回一个表示该关系的位掩码

```
000000    0     两个节点相同
000001    1     两个节点不在同一个文档（即有一个节点不在当前文档）
000010    2     参数节点在当前节点的前面
000100    4     参数节点在当前节点的后面
001000    8     参数节点包含当前节点
010000    16    当前节点包含参数节点
100000    32    浏览器的私有用途
```

```html
<div id="myDiv">
    <ul id="myUl">
        <li id="myLi1"></li>
        <li id="myLi2"></li>
    </ul>
</div>
<script>
    //20=16+4，因为myUl节点被myDiv节点包含，也位于myDiv节点的后面
    console.log(myDiv.compareDocumentPosition(myUl));
    //10=8+2，因为myDiv节点包含myUl节点，也位于myUl节点的前面
    console.log(myUl.compareDocumentPosition(myDiv));
    //0，两个节点相同
    console.log(myDiv.compareDocumentPosition(myDiv));
    //4，myLi2在myLi1节点的后面
    console.log(myLi1.compareDocumentPosition(myLi2));
    //2，myLi1在myLi2节点的前面
    console.log(myLi2.compareDocumentPosition(myLi1));
</script>
```

#### 3.2.2 isSameNode()和isEqualNode()

这两个方法都接受一个节点参数，并在传入节点与引用节点相同或相等时返回true

　　所谓相同(same)，指的是两个节点引用的是同一个对象

　　所谓相等(equal)，指的是两个节点是相同的类型，具有相等的属性(nodeName、nodeValue等等)，而且它们的attributes和childNodes属性也相等(相同位置包含相同的值)

　　[注意]firefox不支持isSameNode()方法，而IE8-浏览器两个方法都不支持

```html
<script>
    var div1 = document.createElement('div');
    div1.setAttribute("title","test");
    var div2 = document.createElement('div');
    div2.setAttribute("title","test");
    console.log(div1.isSameNode(div1));//true
    console.log(div1.isEqualNode(div2));//true
    console.log(div1.isSameNode(div2));//false
</script>
```





## 参考资料

[深入理解DOM节点关系](http://www.cnblogs.com/xiaohuochai/p/5785297.html)

[深入理解DOM节点类型第五篇——元素节点Element](http://www.cnblogs.com/xiaohuochai/p/5819638.html)

[深入理解javascript中的动态集合——NodeList、HTMLCollection和NamedNodeMap](http://www.cnblogs.com/xiaohuochai/p/5827389.html)

