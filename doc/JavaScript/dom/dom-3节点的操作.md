[TOC]

## 1. 描述

DOM提供节点操作的方法是因为DOM节点关系指针都是只读的

　　下列代码中想通过修改myUl的父级节点来修改其节点关系，但由于parentNode属性是只读的，所以修改无效，在IE8-浏览器下甚至会报错

```html
<div id="myDiv"></div>
<ul id="myUl">
    <li id="myli"></li>
</ul>
<script>
    console.log(myUl.parentNode);//<body>
    myUl.parentNode = myDiv;
    //标准浏览器下，依然返回<body>；而IE8-浏览器则会报错
    console.log(myUl.parentNode);
</script>
```

DOM节点操作方法包括创建节点、插入节点、删除节点、替换节点、查看节点和复制节点。查看节点指的是查看节点之间的关系

## 2. 创建节点：createElement()

document.createElement()方法可以创建新元素。这个方法接受一个参数，即要创建元素的标签名，这个标签名在HTML文档中不区分大小写

```
var oDiv = document.createElement("div");
console.log(oDiv);//<div>
```

　　IE8-浏览器可以为这个方法传入完整的元素标签，也可以包含属性

```
var oDiv = document.createElement('<div id="box"></div>');
console.log(oDiv.id);//'box'
```

　　利用这种方法可以避开IE7-浏览器在动态创建元素的下列问题　　

​	1、不能设置动态创建的`<iframe>`元素的name特性

　　2、不能通过表单的reset()方法重设动态创建的`<input>`元素

　　3、动态创建的type特性值为"reset"的`<button>`元素重设不了表单

　　4、动态创建的一批name相同的单选按钮彼此毫无关系。name值相同的一组单选按钮本来应该用于表示同一选项的不同值，但动态创建的一批这种单选按钮之间却没有这种关系

```javascript
var iframe = document.createElement("<iframe name = 'myframe'></iframe>");
var input = document.createElement("<input type='checkbox'>);
var button = document.createElement("<button type = 'reset'></button>");
var radio1 = document.createElement("<input type='radio' name ='choice' value = '1'>");
var radio2 = document.createElement("<input type='radio' name ='choice' value = '2'>");
```

　　所有节点都有一个ownerDocument的属性，指向表示整个文档的文档节点document；在使用createElement()方法创建新元素的同时，也为新元素设置了ownerDocument属性

```html
<div id="myDiv"></div>
<script>
console.log(myDiv.ownerDocument);//document
var newDiv = document.createElement('div');
console.log(newDiv.ownerDocument);//document
console.log(newDiv.ownerDocument === myDiv.ownerDocument);//true
</script>
```

[Document.createElement() MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/Document/createElement)



## 3. 插入节点

### 3.1 appendChild：向childNodes列表的末尾添加一个节点

appendChild()方法用于向childNodes列表的末尾添加一个节点，并返回新增节点。添加节点后，childNodes中的新增节点、父节点和以前的最后一个子节点的关系指针都会相应地得到更新

[Node.appendChild MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/appendChild)

```html
<div id="one"></div>
<script>
    var one = document.getElementById('one');
    var newNode = document.createElement('ul');
    var returnedNode = one.appendChild(newNode);
    console.log(returnedNode.nodeName);//UL
    console.log(returnedNode == newNode);//true
    console.log(returnedNode == one.lastChild);//true
</script>
```

如果插入的节点已经是文档的一部分了，那结果就是将该节点从原来的位置转移到新位置

```html
<div id="oldDiv">第一个div</div>
<div id="newDiv">第二个div</div>
<button id="btn">变换位置</button>
<script>
    btn.onclick = function(){ document.body.appendChild(newDiv); }    
</script>
```

<div id="oldDiv">第一个div</div>
<div id="newDiv">第二个div</div>
<button id="btn">变换位置</button>
<script>
btn.onclick = function(){ document.body.appendChild(newDiv); }    
</script>

### 3.2 Node.insertBefore:父节点中指定子节点前插入

语法：`insertedElement = parentElement.insertBefore(newElement, referenceElement);`

如果`referenceElement`为`null`则`newElement`将被插入到子节点的末尾*。*如果`newElement`已经在DOM树中，`newElement`首先会从DOM树中移除。

> - `insertedElement` 是被插入的节点，即 `newElement`
> - `parentElement`  是新插入节点的父节点
> - `newElement` 是被插入的节点
> - `referenceElement` 在插入newElement之前的那个节点

[Node.insertBefore() MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/insertBefore)

```html
<ul id="myUl" style="border:1px solid black;">
    <li id="myLi">
        <div id='oldDiv'>oldDiv</div>
    </li>    
</ul>
<button id="btn1">插入oldDiv的前面</button>
<button id="btn2">插入myUl的前面</button>
<button id="btn3">插到oldDiv的里面</button>
<script>
var oDiv = document.createElement('div');
oDiv.innerHTML = 'newDiv';
btn1.onclick = function(){
    console.log(myLi.insertBefore(oDiv,oldDiv));//<div>newDiv</div>
}
btn2.onclick = function(){
    console.log(document.body.insertBefore(oDiv,myUl));//<div>newDiv</div>
}
btn3.onclick = function(){
    console.log(oldDiv.insertBefore(oDiv,null));//<div>newDiv</div>
}
</script>
```

<ul id="myUl" style="border:1px solid black;">
    <li id="myLi">
        <div id='oldDiv'>oldDiv</div>
    </li>    
</ul>
<button id="btn1">插入oldDiv的前面</button>
<button id="btn2">插入myUl的前面</button>
<button id="btn3">插到oldDiv的里面</button>
<script>
var oDiv = document.createElement('div');
oDiv.innerHTML = 'newDiv';
btn1.onclick = function(){
    console.log(myLi.insertBefore(oDiv,oldDiv));//<div>newDiv</div>
}
btn2.onclick = function(){
    console.log(document.body.insertBefore(oDiv,myUl));//<div>newDiv</div>
}
btn3.onclick = function(){
    console.log(oldDiv.insertBefore(oDiv,null));//<div>newDiv</div>
}
</script>





## 参考资料

[深入理解DOM节点操作](http://www.cnblogs.com/xiaohuochai/p/5787459.html)