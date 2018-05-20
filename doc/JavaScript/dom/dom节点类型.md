[TOC]

## 1. 节点说明

DOM是javascript操作网页的接口，全称为文档对象模型(Document Object Model)。它的作用是将网页转为一个javascript对象，从而可以使用javascript对网页进行各种操作(比如增删内容)。浏览器会根据DOM模型，将HTML文档解析成一系列的节点，再由这些节点组成一个树状结构。DOM的最小组成单位叫做节点(node)，文档的树形结构(DOM树)由12种类型的节点组成。

一般地，节点至少拥有nodeType、nodeName和nodeValue这三个基本属性。节点类型不同，这三个属性的值也不相同

### 1.1 nodeType

nodeType属性返回节点类型的常数值。不同的类型对应不同的常数值，12种类型分别对应1到12的常数值

```
元素节点            　　Node.ELEMENT_NODE(1)
属性节点            　　Node.ATTRIBUTE_NODE(2)
文本节点            　　Node.TEXT_NODE(3)
CDATA节点             Node.CDATA_SECTION_NODE(4)
实体引用名称节点    　　 Node.ENTRY_REFERENCE_NODE(5)
实体名称节点        　　Node.ENTITY_NODE(6)
处理指令节点        　　Node.PROCESSING_INSTRUCTION_NODE(7)
注释节点            　 Node.COMMENT_NODE(8)
文档节点            　 Node.DOCUMENT_NODE(9)
文档类型节点        　　Node.DOCUMENT_TYPE_NODE(10)
文档片段节点        　　Node.DOCUMENT_FRAGMENT_NODE(11)
DTD声明节点            Node.NOTATION_NODE(12)
```

DOM定义了一个Node接口，这个接口在javascript中是作为Node类型实现的，而在IE8-浏览器中的所有DOM对象都是以COM对象的形式实现的。所以，IE8-浏览器并不支持Node对象的写法

```javascript
//在标准浏览器下返回1，而在IE8-浏览器中报错，提示Node未定义
console.log(Node.ELEMENT_NODE);//1
```

### 1.2 nodeName

nodeName属性返回节点的名称

### 1.3 nodeValue

nodeValue属性返回或设置当前节点的值，格式为字符串

## 2. 节点介绍

| 节点类型         | nodeType | nodeName          | nodeValue                         | Named Constant              |
| ---------------- | -------- | ----------------- | --------------------------------- | --------------------------- |
| 元素节点         | 1        | 标签名（大写）    | null                              | ELEMENT_NODE                |
| 属性节点         | 2        | 属性名            | 属性值                            | ATTRIBUTE_NODE              |
| 文本节点         | 3        | `#text`           | 文本内容                          | TEXT_NODE                   |
| CDTAT节点        | 4        | cdata-section     | CDATA区域的内容                   | CDATA_SECTION_NODE          |
| 实体引用名称节点 | 5        | 引用名称          | null                              | ENTITY_REFERENCE_NODE       |
| 实体名称节点     | 6        | 实体名称          | null                              | ENTITY_NODE                 |
| 处理指令节点     | 7        | target            | entire content cluding the target | PROCESSING_INSTRUCTION_NODE |
| 注释节点         | 8        | `#comment`        | 注释内容                          | COMMENT_NODE                |
| 文档节点         | 9        | `#document`       | null                              | DOCUMENT_NODE               |
| 文档类型节点     | 10       | doctype的名称     | null                              | DOCUMENT_TYPE_NODE          |
| 文档片段节点     | 11       | document-fragment | null                              | DOCUMENT_FRAGMENT_NODE      |
| DTD声明节点      | 12       | 符号名称          | null                              | NOTATION_NODE               |

12 种不同的节点类型，其中可能会有不同节点类型的子节点：

| 节点类型              | 描述                                               | 子节点                                                       |
| --------------------- | -------------------------------------------------- | ------------------------------------------------------------ |
| Element               | 代表元素                                           | Element, Text, Comment, ProcessingInstruction, CDATASection, EntityReference |
| Attr                  | 代表属性                                           | Text, EntityReference                                        |
| Text                  | 代表元素或属性中的文本内容                         | None                                                         |
| CDATASection          | 代表文档中的 CDATA 部分（不会由解析器解析的文本）  | None                                                         |
| EntityReference       | 代表实体引用                                       | Element, ProcessingInstruction, Comment, Text, CDATASection, EntityReference |
| Entity                | 代表实体                                           | Element, ProcessingInstruction, Comment, Text, CDATASection, EntityReference |
| ProcessingInstruction | 代表处理指令                                       | None                                                         |
| Comment               | 代表注释                                           | None                                                         |
| Document              | 代表整个文档（DOM 树的根节点）                     | Element, ProcessingInstruction, Comment, DocumentType        |
| DocumentType          | 向为文档定义的实体提供接口                         | None                                                         |
| DocumentFragment      | 代表轻量级的 Document 对象，能够容纳文档的某个部分 | Element, ProcessingInstruction, Comment, Text, CDATASection, EntityReference |
| Notation              | 代表 DTD 中声明的符号                              | None                                                         |

### 2.1 元素节点

元素节点：对应网页的HTML标签元素。

> nodeType: 1
>
> nodeName: 大写的标签名
>
> nodeValue: null

```javascript
// 1 'BODY' null
console.log(document.body.nodeType,document.body.nodeName,document.body.nodeValue)
console.log(Node.ELEMENT_NODE === 1);//true
```

### 2.2 属性节点

属性节点：对应网页中HTML标签的属性，它只存在于元素的attributes属性中，并不是DOM文档树的一部分。

> nodeType: 2
>
> nodeName: 属性名
>
> nodeValue: 属性值

```html
<div id="test"></div>
<script>
    var attr = test.attributes.id;
    //2 'id' 'test'
    console.log(attr.nodeType,attr.nodeName,attr.nodeValue)
    console.log(Node.ATTRIBUTE_NODE === 2);//true    
</script>
```

### 2.3 文本节点

文本节点：网页中的HTML标签内容。

> nodeType: 3
>
> nodeName:  `#text`
>
> nodeValue: 标签内容值

```html
<div id="test">测试</div>
<script>
    var txt = test.firstChild;
    //3 '#text' '测试'
    console.log(txt.nodeType,txt.nodeName,txt.nodeValue)
    console.log(Node.TEXT_NODE === 3);//true    
</script>
```

### 2.4 注释节点

表示网页中的HTML注释。

> nodeType: 8
>
> nodeName:  `#comment`
>
> nodeValue: 注释的内容

```html
<div id="myDiv"><!-- 我是注释内容 --></div>
<script>
    var com = myDiv.firstChild;
    //8 '#comment' '我是注释内容'
    console.log(com.nodeType,com.nodeName,com.nodeValue)
    console.log(Node.COMMENT_NODE === 8);//true    
</script>
```

### 2.5 文档节点

表示HTML文档，也称为根节点，指向document对象。

> nodeType: 9
>
> nodeName:  `#document`
>
> nodeValue:  null

```html
<script>
//9 "#document" null
console.log(document.nodeType,document.nodeName,document.nodeValue)
console.log(Node.DOCUMENT_NODE === 9);//true    
</script>
```

### 2.6 文档类型节点

包含着与文档的doctype有关的所有信息。

> nodeType: 10
>
> nodeName:  doctype的名称
>
> nodeValue:  null

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Document</title>
    </head>
    <body>
        <script>
            var nodeDocumentType = document.firstChild;
            //10 "html" null
        console.log(nodeDocumentType.nodeType,nodeDocumentType.nodeName,nodeDocumentType.nodeValue);
            console.log(Node.DOCUMENT_TYPE_NODE === 10);
        </script>
    </body>
</html>
```



### 2.7 文档片段节点

在文档中没有对应的标记，是一种轻量级的文档，可以包含和控制节点，但不会像完整的文档那样占用额外的资源。

> nodeType: 11
>
> nodeName:  `#document-fragment`
>
> nodeValue:  null

```html
<script>
var nodeDocumentFragment = document.createDocumentFragment();    
//11 "#document-fragment" null
console.log(nodeDocumentFragment.nodeType,nodeDocumentFragment.nodeName,nodeDocumentFragment.nodeValue);
console.log(Node.DOCUMENT_FRAGMENT_NODE === 11);//true
</script>
```

### 2.8 DTD声明节点

DTD声明节点notation代表DTD中声明的符号。

> nodeType: 12
>
> nodeName:  符号名称
>
> nodeValue:  null







## 参考资料

[DOM常用节点类型](https://blog.csdn.net/u013243347/article/details/52122958)

[简述HTML DOM及其节点分类](http://www.cnblogs.com/zhuwq585/p/6075119.html)

[深入理解DOM节点类型第一篇——12种DOM节点类型概述](http://www.cnblogs.com/xiaohuochai/p/5785189.html)

