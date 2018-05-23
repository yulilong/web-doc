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

1、不能设置动态创建的`<iframe>`元素的name特性

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

### 3.1 appendChild()：向childNodes列表的末尾添加一个节点

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



### 3.2 Node.insertBefore():父节点中指定子节点前插入

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
// //<div>newDiv</div> 三个输出都一样
btn1.onclick = function(){ console.log(myLi.insertBefore(oDiv,oldDiv)); }
btn2.onclick = function(){ console.log(document.body.insertBefore(oDiv,myUl)); }
btn3.onclick = function(){ console.log(oldDiv.insertBefore(oDiv,null)); }
</script>
```

一个效果：

```html
<ul class="list" id="list">
    <li class="in">1</li> <li class="in">2</li> <li class="in">3</li>
    <li class="in">4</li> <li class="in">5</li> <li class="in">6</li>        
</ul>
<script>
    var oList = document.getElementById('list');
    //新增一个li元素
    var oAdd = document.createElement('li');
    //设置新增元素的css样式
    oAdd.className = "in";
    oAdd.style.cssText = 'background-color:red;border-radius:50%';
    //添加到oList中
    oList.insertBefore(oAdd,null);
    var num = -1;
    var max = oList.children.length;
    function incrementNumber(){
        num++;
        //oList.getElementsByTagName('li')[max]相当于null，所以不报错
        oList.insertBefore(oAdd,oList.getElementsByTagName('li')[num]);    
        if(num == max){ num = -1; }    
        if(num == 0){ num = 1; }
        setTimeout(incrementNumber,1000);
    }
    setTimeout(incrementNumber,1000);
</script>
```



### 3.3 自己实现insertAfter

由于不存在insertAfter()方法，如果要插在当前节点的某个子节点后面，可以用insertBefore()和appendChild()封装方法

```html
<div id='oldDiv'>old</div>
<button id="btn">增加节点</button>
<script>
    function insertAfter(newElement,targetElement){
        var parent = targetElement.parentNode;
        if(parent.lastChild == targetElement){
            return parent.appendChild(newElement);
        }else{
            return parent.insertBefore(newElement,targetElement.nextSibling)
        }
    }    
    var newDiv = document.createElement('div');
    newDiv.innerHTML = 'new';
    btn.onclick = function(){ insertAfter(newDiv,oldDiv); }
</script>
```

### 3.4 element.insertAdjacentHTML():将文本解析为HTML

**insertAdjacentHTML()** 将指定的文本解析为HTML或XML，并将结果节点插入到DOM树中的指定位置。它不会重新解析它正在使用的元素，因此它不会破坏元素内的现有元素。这避免了额外的序列化步骤，使其比直接innerHTML操作更快。

语法：`element.insertAdjacentHTML(position, text);`

> position是相对于元素的位置，并且必须是以下字符串之一：
>
> ```
> 'beforebegin':元素自身的前面
> 'afterbegin': 插入元素内部的第一个子节点之前
> 'beforeend': 插入元素内部的最后一个子节点之后
> 'afterend': 元素自身的后面。
> ```
>
> text是要被解析为HTML或XML,并插入到DOM树中的字符串,如果浏览器无法解析字符串，就会抛出错误

其中position的示例：

```html
<!-- beforebegin --> 
<p> 
<!-- afterbegin -->
foo
<!-- beforeend -->
</p>
<!-- afterend -->
```

[element.insertAdjacentHTML MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/Element/insertAdjacentHTML)

一个例子：

```html
<div id='target' style="border: 1px solid black;">This is the element content</div>
<button>beforebegin</button>
<button>afterbegin</button>
<button>beforeend</button>
<button>afterend</button>
<script>
    var btns = document.getElementsByTagName('button');
    for(var i = 0 ; i < 4; i++){
        btns[i].onclick = function(){
            var that = this;
            target.insertAdjacentHTML(that.innerHTML,'<span id="test">测试</span>')    
        }
    }
</script> 
```



## 4. 移除节点

### 4.1 Node.removeChild()：删除一个子节点返回删除的节点

removeChild()方法接收一个参数，即要移除的节点，被移除的节点成为方法的返回值

语法：

```javascript
let oldChild = node.removeChild(child);
//或者
element.removeChild(child);
```

- `child` 是要移除的那个子节点.
- `node` 是`child`的父节点.
- oldChild保存对删除的子节点的引用. `oldChild` === `child`.

 被移除的这个子节点仍然存在于内存中,只是没有添加到当前文档的DOM树中,因此,你还可以把这个节点重新添加回文档中,当然,实现要用另外一个变量比如`上例中的oldChild`来保存这个节点的引用. 如果使用上述语法中的第二种方法, 即没有使用 oldChild 来保存对这个节点的引用, 则认为被移除的节点已经是无用的, 在短时间内将会被[内存管理](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Memory_Management)回收.

如果上例中的`child节点`不是`node`节点的子节点,则该方法会抛出异常.

[Node.removeChild MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/removeChild)

例子：

```html
<div id="myDiv">等待移除的节点</div>
<button id="btn">移除节点</button>
<script>
    btn.onclick = function(){ document.body.removeChild(myDiv); }
</script>
```

移除当前节点的所有子节点:

```javascript
var element = document.getElementById("top");
while (element.firstChild) {
  element.removeChild(element.firstChild);
}
```

一个效果：点击按钮删除所有子节点：

```html
<button id="btn">开始删除节点</button>
<ul class="list" id="list">
    <li class="in">1</li> <li class="in">2</li> <li class="in">3</li>
    <li class="in">4</li> <li class="in">5</li> <li class="in">6</li>        
</ul>
<script>
    var oList = document.getElementById('list');
    function incrementNumber(){
        //获取oList中子元素的个数
        var len = oList.getElementsByTagName('li').length;
        //如果长度不为0
        if(len){
            //删除最后一个子元素
            oList.removeChild(oList.getElementsByTagName('li')[len-1]);
            //再次调用计时器
            setTimeout(incrementNumber,1000);    
        }
    }
    btn.onclick = function(){
        //1s后执行函数incrementNumber
        setTimeout(incrementNumber,1000);    
    }
</script>
```

### 4.2 ChildNode.remove():从它所属的DOM树中删除对象

相比于removeChild()，remove()方法不太常见，但是却非常简单。该方法不用调用其父节点，直接在当前节点使用remove()方法就可以删除该节点，无返回值

remove()方法常用于删除[元素节点](http://www.cnblogs.com/xiaohuochai/p/5819638.html)和[文本节点](http://www.cnblogs.com/xiaohuochai/p/5815193.html)，不可用于[特性节点](http://www.cnblogs.com/xiaohuochai/p/5820076.html)

[注意]IE浏览器不支持该方法

```html
<div id="test" title='div'>123</div>
<script>
    //文本节点
    console.log(test.childNodes[0]);//'123'
    test.childNodes[0].remove();
    console.log(test.childNodes[0]);//undefined

    //特性节点
    console.log(test.attributes.title);//'div'
    //报错，remove()方法无法用于删除特性节点
    try{test.attributes[0].remove()}catch(e){
        console.log('error');
    }
    //元素节点
    console.log(test);
    test.remove();
</script>
```

## 5. 替换节点：Node.replaceChild()

用指定的节点替换当前节点的一个子节点，并返回被替换掉的节点。

语法：

```javascript
replacedNode = parentNode.replaceChild(newChild, oldChild);
```

- `newChild `用来替换 `oldChild `的新节点。如果该节点已经存在于DOM树中，则它会被从原始位置删除。
- `oldChild`  被替换掉的原始节点。
- `replacedNode` 和`oldChild相等`。

 [Node.replaceChild() MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/replaceChild)

一个例子：

```html
<div id="div1">1</div>
<div id="div2">2</div>
<div id="div3">3</div>
<button id="btn1">新增节点替换(4替换2)</button>
<button id="btn2">原有节点替换(3替换1)</button>
<script>
    btn2.onclick = function(){
        document.body.replaceChild(div3,div1);
    }
    btn1.onclick = function(){
        var div4 = document.createElement('div');
        div4.innerHTML = '4';
        document.body.replaceChild(div4,div2);
    }
</script>
```

## 6. 复制节点：Node.cloneNode()

**Node.cloneNode()** 方法返回调用该方法的节点的一个副本.

语法：

```javascript
var dupNode = node.cloneNode(deep);
```

> node: 将要被克隆的节点
>
> dupNode: 克隆生成的副本节点
>
> deep(可选): 是否采用深度克隆`,如果为true,`则该节点的所有后代节点也都会被克隆,如果为`false,则只克隆该节点本身.`

[注意]cloneNode()方法不会复制添加到DOM节点中的javascript属性，例如事件处理程序等。这个方法只复制特性和子节点，其他一切都不会复制

[Node.cloneNode MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/cloneNode)

一个例子：

```html
<ul id="list">
    <li>1</li> <li>2</li> <li>3</li>
    <li>4</li> <li>5</li> <li>6</li>        
</ul>
<script>
    var oList = document.getElementById('list');
    oList.index = 0;
    var deepList = oList.cloneNode(true);
    //成功复制了子节点
    console.log(deepList.children.length);//6
    //但并没有复制属性
    console.log(deepList.index);//undefined
    var shallowList = oList.cloneNode();
    //浅复制不复制子节点
    console.log(shallowList.children.length);//0
</script>
```





## 参考资料

[深入理解DOM节点操作](http://www.cnblogs.com/xiaohuochai/p/5787459.html)

[深入理解DOM节点类型第一篇——12种DOM节点类型概述](https://www.cnblogs.com/xiaohuochai/p/5785189.html)

[深入理解DOM节点类型第二篇——文本节点Text](https://www.cnblogs.com/xiaohuochai/p/5815193.html)

[深入理解DOM节点类型第三篇——注释节点和文档类型节点](https://www.cnblogs.com/xiaohuochai/p/5815801.html)

[深入理解DOM节点类型第四篇——文档片段节点DocumentFragment](https://www.cnblogs.com/xiaohuochai/p/5816048.html)

[深入理解DOM节点类型第五篇——元素节点Element](https://www.cnblogs.com/xiaohuochai/p/5819638.html)

[深入理解DOM节点类型第六篇——特性节点Attribute](https://www.cnblogs.com/xiaohuochai/p/5820076.html)

[深入理解DOM节点类型第七篇——文档节点DOCUMENT](https://www.cnblogs.com/xiaohuochai/p/5821803.html)



[深入理解javascript描述元素内容的5个属性](https://www.cnblogs.com/xiaohuochai/p/5823716.html)

[深入理解javascript中的动态集合——NodeList、HTMLCollection和NamedNodeMap](https://www.cnblogs.com/xiaohuochai/p/5827389.html)

[深入理解定位父级offsetParent及偏移大小](https://www.cnblogs.com/xiaohuochai/p/5828369.html)

[了解screen对象的常用视图属性](https://www.cnblogs.com/xiaohuochai/p/5829959.html)

[深入理解客户区尺寸client](https://www.cnblogs.com/xiaohuochai/p/5830053.html)

[深入理解滚动scroll](https://www.cnblogs.com/xiaohuochai/p/5831640.html)

[区分元素特性attribute和对象属性property](https://www.cnblogs.com/xiaohuochai/p/5817608.html)

[5种回到顶部的写法从实现到增强](https://www.cnblogs.com/xiaohuochai/p/5836179.html)

