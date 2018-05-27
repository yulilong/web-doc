[TOC]

javascript中的动态集合——NodeList、HTMLCollection和NamedNodeMap



## 1. NodeList

`NodeList` 对象是一个节点的集合，是由 `Node.childNodes` 和 document.querySelectorAl返回的.

- 属性

  > length： NodeList 对象中包含的节点个数.

- 方法

  > item ( idx ):返回NodeList对象中指定索引的节点,如果索引越界,则`返回null`.等价的写法是`nodeList[idx], 不过这种情况下越界访问将返回undefined.`

```html
<div id="one"><span>1</span></div>
<script>
  console.log(one.childNodes.length)	// 1
  console.log(one.childNodes.item(0))	// <span>1</span>
  console.log(one.childNodes[0])		// <span>1</span>
</script>
```

### 1.1 Node.childNodes返回动态集合 

Node.childNodes返回的`NodeList `对象是个`实时集合`。也就是说文档中的节点树发生变化，则已经存在的 NodeList 对象也会变化。

下面的例子中，在添加一个节点后，NodeList 对象也实时的增加了：

```html
<div id="one"><span>1</span></div>
<script>
    var child_nodes = one.childNodes;
    console.log(child_nodes.length);	// 1
    one.appendChild(document.createElement('div'));
    console.log(child_nodes.length); 	// 2
</script>
```

### 1.2 document.querySelectorAll()返回静态集合 

document.querySelectorAll()返回的`NodeList `对象是个静态的。也就是说文档中节点树发生变化，已存在的NodeList 对象不会变化。

下面的例子中添加了一个节点，但是NodeList 对象没有变化:

```html
<div class="one"><span>1</span></div>
<script>
  var one = document.querySelector(".one")
  var child_nodes = one.querySelectorAll("span");// NodeList [span]
  console.log(child_nodes.length)						// 1
  one.appendChild(document.createElement('span'));		// 添加了一个节点
  console.log(child_nodes.length); 						// 1
  console.log(one.querySelectorAll("span").length);		// 2
</script>
```

### 1.3 NodeList是类数组对象

NodeList是类数组对象,不是数组,除了`forEach`方法，NodeList 没有这些类似数组的方法。

注意：forEach方法有的浏览器不支持(QQ浏览器老版本、IE8以前)。

JavaScript 的继承机制是基于原型的。数组元素之所以有一些数组方法（比如` forEach `和 `map）`，是因为它的原型链上有这些方法，如下:

`myArray --> Array.prototype --> Object.prototype --> null (想要获取一个对象的原型链，可以连续的调用 Object.getPrototypeOf，直到原型链尽头).`

`forEach`, `map`这些方式其实是` Array.prototype` 这个对象的方法。

和数组不一样`，NodeList`的原型链是这样的：

`myNodeList --> NodeList.prototype --> Object.prototype --> null`

NodeList的原型上除了类似数组的`forEach`方法之外，还有`item`，`entries`，`keys`和`values`方法。

### 1.4 遍历NodeList对象方法 

- 将NodeList对象转为数组

  ```javascript
  var div_list = document.querySelectorAll('div'); // 返回 NodeList
  
  var div_array = Array.prototype.slice.call(div_list); // 将 NodeList 转换为数组
  
  //ES6 - Array.from();
  var div_array_from = Array.from(div_list); //将 NodeList 转换为数组
  ```

  由于IE8-浏览器将NodeList实现为一个COM对象，不能使用Array.prototype.slice()方法，必须手动枚举所有成员

- 直接使用Array的forEach方法

  ```javascript
  var forEach = Array.prototype.forEach;
  
  var divs = document.getElementsByTagName( 'div' );
  var firstDiv = divs[ 0 ];
  
  forEach.call(firstDiv.childNodes, function( divChild ){
    divChild.parentNode.style.color = '#0F0';
  });
  ```

  请注意，在上面的代码中，将某个宿主对象 （如` NodeList`） 作为 `this` 传递给原生方法 （如 forEach） 不能保证在所有浏览器中工作，已知在一些浏览器中会失败。

- 使用for循环

  ```javascript
  for (var i = 0; i < myNodeList.length; ++i) {
    var item = myNodeList[i];  // 调用 myNodeList.item(i) 是没有必要的
  }
  ```



## 2. HTMLCollection

**HTMLCollection** 接口表示一个包含了元素（元素顺序为文档流中的顺序）的通用集合（generic collection），还提供了用来从该集合中选择元素的方法和属性。

- 属性

  > length： 只读，返回集合当中子元素的数目。

- 方法

  > item ( idx ): 
  >
  > 根据给定的索引（从0开始），返回具体的节点。如果索引超出了范围，则返回 `null`。
  >
  > namedItem(): 
  >
  > 根据 Id 返回指定节点，或者作为备用，根据字符串所表示的 `name` 属性来匹配。根据 name 匹配只能作为最后的依赖，并且只有当被引用的元素支持 `name` 属性时才能被匹配。如果不存在符合给定 name 的节点，则返回 `null`。

```html
<input type="text" name="mac" id="mm">
<script>
  cc = document.getElementsByTagName("input");	
  // HTMLCollection [input#mm, mm: input#mm, mac: input#mm]
  cc.namedItem("mac")	// <input type="text" name="mac" id="mm">
  console.log(cc.namedItem('mm'));	// <input type="text" name="mac" id="mm">
  console.log(cc.length);	// 1
  console.log(cc.item(0))	// <input type="text" name="mac" id="mm">
</script>
```

HTMLCollection对象与NodeList对象类似，也是节点的集合，返回一个类数组对象。

NodeList集合主要是Node节点的集合，而HTMLCollection集合主要是Element元素节点的集合。Node节点共有12种，Element元素节点只是其中一种。

HTMLCollection集合包括getElementsByTagName()、getElementsByClassName()、getElementsByName()等方法的返回值，以及children、document.links、document.forms等元素集合



HTML DOM 中的 `HTMLCollection` 是即时更新的（live）；当其所包含的文档结构发生改变时，它会自动更新。

```html
<div id="test"></div>
<script>
    var childN = test.children;
    var tags =test.getElementsByTagName('div');
    console.log(childN,tags);//[]、[]
    test.innerHTML = '<div></div>';
    console.log(childN,tags);//[div]、[div]
</script>   
```

[注意]与NodeList对象类似，要想变成真正的数组Array对象，需要使用slice()方法，在IE8-浏览器中，则必须手动枚举所有成员

## 3. NamedNodeMap

NamedNodeMap 接口表示属性节点 [`Attr`](https://developer.mozilla.org/zh-CN/docs/Web/API/Attr) 对象的集合。尽管在 `NamedNodeMap` 里面的对象可以像数组一样通过索引来访问，但是它和 [`NodeList`](https://developer.mozilla.org/zh-CN/docs/Web/API/NodeList) 不一样，对象的顺序没有指定。

`NamedNodeMap` 对象是即时的(*live*)，因此，如果它内部包含的对象发生改变的话，该对象会自动更新到最新的状态。

- 属性: *该接口没有继承任何属性。*

  > length: 只读， 返回映射(map)中对象的数量。

- 方法

  > getNamedItem() : 返回一个给定名字对应的属性节点
  >
  > setNamedItem(): 替换或添加一个属性节点到映射（map）中。
  >
  > removeNamedItem(): 移除一个属性节点
  >
  > item(): 返回指定索引处的属性节点，当索引超出或等于属性节点的数量时，返回 `null`

```html
<style type="text/css">
.democlass{ color:red; }
</style>
<div id="test" datat-tt="pp">123</div>
<script>
    var att = test.attributes;	
    // NamedNodeMap {0: id, 1: datat-tt, 2: class, id: id,
    console.log(att.length);	// 2
    
    console.log(att.getNamedItem('id'));	// id="test"
    var typ=document.createAttribute("class");
    typ.nodeValue="democlass";
    att.setNamedItem(typ);	// 此时页面上字体会变红
    att.removeNamedItem('class');// class="democlass" 此时类已经删除了，颜色恢复了
    att.item(0);	// id="test"
    
</script>   
```

该对象也是一个动态集合:

```html
<div id="test"></div>
<script>
    var attrs = test.attributes;
    console.log(attrs);//NamedNodeMap {0: id, length: 1}
    test.setAttribute('title','123');
    console.log(attrs);//NamedNodeMap {0: id, 1: title, length: 2}
</script>
```



## 4. 遍历动态集合注意事项

动态集合是个很实用的概念，但在使用循环时一定要千万小心。可能会因为忽略集合的动态性，造成死循环

```java
var divs = document.getElementsByTagName("div");
for(var i = 0 ; i < divs.length; i++){
    document.body.appendChild(document.createElement("div"));
}
```

在上面代码中，由于divs是一个HTMLElement集合，divs.length会随着appendChild()方法，而一直增加，于是变成一个死循环

　　为了避免此情况，一般地，可以写为下面形式

```javascript
var divs = document.getElementsByTagName("div");
for(var i = 0,len = divs.length; i < len; i++){
    document.body.appendChild(document.createElement("div"));
}
```

 　　一般地，要尽量减少访问NodeList、HTMLCollection、NamedNodeMap的次数。因为每次访问它们，都会运行一次基于文档的查询。所以，可以考虑将它们的值缓存起来





## 参考资料

[Node.childNodes](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/childNodes) 

[document.querySelectorAll](https://developer.mozilla.org/zh-CN/docs/Web/API/Document/querySelectorAll)

[NodeList MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/NodeList)

[HTMLCollection  MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLCollection)

[Attr MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/Attr)

[深入理解javascript中的动态集合——NodeList、HTMLCollection和NamedNodeMap](http://www.cnblogs.com/xiaohuochai/p/5827389.html)

