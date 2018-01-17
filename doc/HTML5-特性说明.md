## 一、HTML5介绍   

[HTML5](http://www.html5tricks.com/what-is-html5.html)是最新一代的HTML标准，它不仅拥有HTML中所有的特性，而且增加了许多实用的特性，如视频、音频、画布（canvas）等。2012年12月17日，万维网联盟（W3C）正式宣布凝结了大量网络工作者心血的HTML5规范已经正式定稿。根据W3C的发言稿称：“HTML5是开放的Web网络平台的奠基石。”     

HTML5 是定义 HTML 标准的最新的版本。 该术语表示两个不同的概念：    

* 它是一个新版本的HTML语言，具有新的元素，属性和行为。      
* 它有更大的技术集，允许更多样化和强大的网站和应用程序。这个集合有时称为HTML5和朋友，通常缩写为HTML5。      

## 二、HTML5的基本特征    

### 1、向前兼容性   

> 核心理念——平滑过渡！        
不支持html5的浏览器可以向前兼容，并不会影响web内容的显示！     
所有现代浏览器都支持 HTML5。      
此外，所有浏览器，不论新旧，都会自动把未识别元素当做行内元素来处理。      

### 2、跨平台运行性    

[HTML5](http://www.w3school.com.cn/html/html5_intro.asp) 是跨平台的，被设计为在不同类型的硬件（PC、平板、手机、电视机等等）之上运行。    
只要用户的设备支持HTML5，基于HTML5的web程序就可以无障碍的运行！      

### 3、简单易用性     

相对HTML4.01，HTML5更加简单实用，没有XHTML2.0那样严格的语法规则。       

#### 3.1、简化的DOCTYPE声明   

HTML4.01标准版本的DOCTYPE的声明     
```
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://ww.w3.org/TR/html4/strict.dtd"> 
```    

HTML4.01基于框架的HTML文档版本的DOCTYPE的声明     
```
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Frameset//EN" "http://ww.w3.org/TR/html4/frameset.dtd"> 
```

HTML5中的DOCTYPE声明(对字母大小写不敏感)     
```
<!DOCTYPE HTML>
```    

3.2、简化的编码字符集     

对于HTML4.01标准编码字符集声明     
```
<meta http = "Content-Type" content = "text/html;chatset = utf-8">
```    

HTML5的编码字符集声明    
```
<metachatset = "utf-8">
```    

3.3、简化的样式表和脚本引入    

HTML4.01标准的html文档中引入的样式表和脚本文本      
```
<link href = "test.css" type = "text/css" rel = "stylesheet"> 
<script src = "test.js" type = "text/javascript"></script>
```    

HTML5中标准的html文档引入的样式文本和脚本文本     
```
<link href = "test.css" rel = "stylesheet">
<script src = "test.js"></scritpt>
```   

### 4、用户友好性    

强化web页面的变现性能：Audio、video、canvas 等标签元素的引入。   
提高用户体验度：地理位置服务、本地数据存储、文件上传、离线应用等新特性。         

参考资料：https://www.cnblogs.com/zxjwlh/p/4460330.html     

## 三、HTML5新特性   

### 1、新增标签   

* 新增段落和提纲      

> HTML5中新的提纲和节段元素一览:`<section>`,`<article>`,`<nav>`,`<header>`,`<footer>`,`<aside>`和`<hgroup>`. 

* 新的语义标签    

> `<mark>`，`<figure>`，`<figcaption>`，`<data>`，`<time>`，`<output>`，`<progress>`，或者`<meter>`和`<main>`，     
> 这增加了有效的 HTML5 元素的数量。    

* 嵌入视频和音频   

> `<audio> 和 <video>`元素嵌入和允许操作新的多媒体内容。    

* 增强表单控件类型      

> HTML5中对web表单的改进：强制验证 API，一些新的属性，`<input>`属性type的一些新值:     
> `calendar、date、time、email、url、search`    
> 新的 <output> 元素。

* 改进`<iframe>`     

> 使用`sandbox`、`seamless`和`srcdoc`属性，作者们现在可以精确控制`<iframe>`元素的安全级别以及期望的渲染。

* 直接嵌入数学公式     

> `<MathML>`允许直接嵌入数学公式。      

### 2、通信升级： 能够使客户端和服务器之间通过创新的技术方法进行通信      

* Web Sockets（全双工通信协议）   
> 允许在页面和服务器之间建立持久连接并通过这种方法来交换非 HTML 数据。     

* [Server-sent events](https://developer.mozilla.org/zh-CN/docs/Server-sent_events/Using_server-sent_events)（服务器推送）    
> 允许服务器向客户端推送事件，而不是仅在响应客户端请求时服务器才能发送数据的传统范式。    

* [WebRTC](https://developer.mozilla.org/zh-CN/docs/WebRTC) (网页实时通信)     
> 这项技术，其中的 RTC 代表的是即时通信，允许连接到其他人，直接在浏览器中控制视频会议，而不需要一个插件或是外部的应用程序。     

### 3、离线 & 存储：能够让网页在客户端本地存储数据以及更高效地离线运行      

HTML5提供了网页存储的API，方便Web应用的离线使用。除此之外，新的API相对于cookie也有着高安全性，高效率，更大空间等优点。     
HTML5离线存储包含 应用程序缓存，本地存储，索引数据库，文件接口。     

#### 3.1、应用程序缓存（Application Cache）    

使用HTML5，通过创建cache manifest文件，可以轻松地创建web应用的离线版本。     
HTML5引入了应用程序缓存，这意味着 web 应用可进行缓存，并可在没有因特网连接时进行访问。      
应用程序缓存为应用带来三个优势：   
> 1. 离线浏览 – 用户可在应用离线时使用它们     
> 2. 速度 – 已缓存资源加载得更快    
> 3. 减少服务器负载 – 浏览器将只从服务器下载更新过或更改过的资源。   

#### 3.2、本地存储（Local Storage）     

在HTML5中，本地存储是一个window的属性，包括localStorage和sessionStorage。      
从名字应该可以很清楚的辨认二者的区别，前者是一直存在本地的，后者只是伴随着session，窗口一旦关闭就没了。    
localStorage和sessionStorag的存储大小官方建议是每个网站5MB，
Cookies自然是大家都知道，问题主要就是太小，大概也就4KB的样子。     

#### 3.3、索引数据库（Indexed DB）    

IndexedDB允许用户在浏览器中保存大量的数据。     
任何需要发送大量数据的应用都可以得益于这个特性，可以把数据存储在用户的浏览器端，当前这只是IndexedDB的其中一项功能。     
IndexedDB也提供了强大的基于索引的搜索api功能以获得用户所需要的数据。       

#### 3.4、web 应用程序中使用文件    

在之前我们操作本地文件都是使用flash、silverlight或者第三方的activeX插件等技术。      
由于使用了这些技术后就很难进行跨平台、或者跨浏览器、跨设备等情况下实现统一的表现，    
从另外一个角度来说就是让我们的web应用依赖了第三方的插件，而不是很独立，不够通用。     
> 在HTML5标准中，默认提供了操作文件的API让这一切直接标准化。     
> 有了操作文件的API，让我们的Web应用可以很轻松的通过JS来控制文件的读取、写入、文件夹、文件等一系列的操作。   

#### 3.5、在线和离线事件（online and offline）     

Firefox 3 支持 WHATWG 在线和离线事件，这可以让应用程序和扩展检测是否存在可用的网络连接，以及在连接建立和断开时能感知到。      

### 4、多媒体：使 Web 原生支持音视频播放     

* HTML5音视频    
> `<audio>`和`<video>`元素嵌入并支持新的多媒体内容的操作。

* [WebRTC](https://developer.mozilla.org/zh-CN/docs/WebRTC)    
> 这项技术，其中的 RTC 代表的是即时通信，允许连接到其他人，在浏览器中直接控制视频会议，而不需要一个插件或是外部的应用程序。    

* [Camera API](https://developer.mozilla.org/zh-CN/docs/Web/Guide/API/Camera)    
> 允许使用，操作计算机摄像头，并从中存储图像。    

* Track 和 WebVTT     
> `<track>`元素支持字幕和章节。WebVTT 一个文本轨道格式。    

### 5、2D/3D 绘图 & 效果：提供了一个更加分化范围的呈现选择       

#### 5.1、[画布（Canvas）](https://developer.mozilla.org/zh-CN/docs/Web/API/Canvas_API/Tutorial)     

HTML5 的 canvas 元素使用 JavaScript 在网页上绘制图像。      
画布是一个矩形区域，您可以控制其每一像素。     
canvas 拥有多种绘制路径、矩形、圆形、字符以及添加图像的方法。     
HTML5文本API现在由`<canvas>`元素支持。

#### 5.2、[网页图形库（WebGL）](https://developer.mozilla.org/zh-CN/docs/Web/API/WebGL_API)     

WebGL（全写Web Graphics Library）是一种3D绘图标准，这种绘图技术标准允许把JavaScript和OpenGL ES 2.0结合在一起，通过增加OpenGL ES 2.0的一个JavaScript绑定，WebGL可以为HTML5 Canvas提供硬件3D加速渲染，这样Web开发人员就可以借助系统显卡来在浏览器里更流畅地展示3D场景和模型了，还能创建复杂的导航和数据视觉化。显然，WebGL技术标准免去了开发网页专用渲染插件的麻烦，可被用于创建具有复杂3D结构的网站页面，甚至可以用来设计3D网页游戏等等。        
demo：http://www.oschina.net/news/26547/webgl-chrome/    

#### 5.3、[可缩放矢量图形（SVG](https://developer.mozilla.org/zh-CN/docs/Web/SVG)     

一个基于 XML 的可以直接嵌入到 HTML 中的矢量图像格式。    
SVG是用于描述二维矢量图形的一种图形格式。     
与其他图像格式相比，使用 SVG 的优势在于：    
> -SVG 可被非常多的工具读取和修改（比如记事本）     
> -SVG 与 JPEG 和 GIF 图像比起来，尺寸更小，且可压缩性更强      
> -SVG 是可伸缩的      
> -SVG 图像可在任何的分辨率下被高质量地打印       
> -SVG 可在图像质量不下降的情况下被放大     
> -SVG 图像中的文本是可选的，同时也是可搜索的（很适合制作地图）     
> -SVG 可以与 Java 技术一起运行      
> -SVG 是开放的标准       
> -SVG 文件是纯粹的 XML        

### 6、性能 & 集成：提供了非常显著的性能优化和更有效的计算机硬件使用   

* [网页后台任务（Web Workers）](https://developer.mozilla.org/zh-CN/docs/Web/API/Web_Workers_API)     

当在 HTML 页面中执行脚本时，页面的状态是不可响应的，直到脚本已完成。       

Ajax向服务器端发送请求，是异步接收响应的。不然页面会卡住。    

Web Workers 是运行在浏览器后台的 JavaScript，独立于其他脚本，不会影响页面的性能。您可以继续做任何愿意做的事情：点击、选取内容等等，而此时 Web Workers 在后台运行。    

* [XMLHttpRequest](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest) Level 2   
允许异步读取页面的某些部分，允许其显示动态内容，根据时间和用户行为而有所不同。这是在[Ajax](https://developer.mozilla.org/zh-CN/docs/Web/Guide/AJAX)背后的技术。    

* 即时编译的 JavaScript 引擎   
新一代的 JavaScript 引擎功能更强大，性能更杰出。    

* History API     
允许对浏览器历史记录进行操作。这对于那些交互地加载新信息的页面尤其有用。    

* [contentEditable 属性：把你的网站改变成 wiki !](https://developer.mozilla.org/zh-CN/docs/Web/Guide/HTML/Content_Editable)     
页面元素可编辑，HTML5 已经把 contentEditable 属性标准化了。    

* [拖放 API(Drag and Drop API)](https://developer.mozilla.org/zh-CN/docs/Web/API/HTML_Drag_and_Drop_API)     
HTML5 的拖放 API 能够支持在网站内部和网站之间拖放项目。同时也提供了一个更简单的供扩展和基于 Mozilla 的应用程序使用的 API。     

* [HTML 中的焦点管理](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Focus_management_in_HTML)    
支持新的 HTML5 `activeElement`和`hasFocus`属性。     

* [基于 Web 的协议处理程序](https://developer.mozilla.org/zh-CN/docs/Web/API/Navigator/registerProtocolHandler/Web-based_protocol_handlers)     
你现在可以使用`navigator.registerProtocolHandler()`方法把 web 应用程序注册成一个协议处理程序。    

* [requestAnimationFrame](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/requestAnimationFrame)     
允许控制动画渲染以获得更优性能。    

* 全屏API     
为一个网页或者应用程序控制使用整个屏幕，而不显示浏览器界面。    

* [指针锁定 API](https://developer.mozilla.org/zh-CN/docs/API/Pointer_Lock_API)    
允许锁定到内容的指针，这样游戏或者类似的应用程序在指针到达窗口限制时也不会失去焦点。    

### 7、样式设计：全面支持CSS3    

* 新的背景样式特性   
> 现在可以使用`box-shadow`给逻辑框设置一个阴影，而且还可以设置 多背景。   

* 更精美的边框  
> 现在不仅可以使用图像来格式化边框，使用`border-image`和它关联的普通属性，而且可以通过`border-radius`属性来支持圆角边框。    

* 为你的样式设置动画   
> 使用 CSS Transitions 以在不同的状态间设置动画，或者使用 CSS Animations 在页面的某些部分设置动画而不需要一个触发事件，你现在可以在页面中控制移动元素了。    

* 排版方面的改进   
> - 文字溢出`text-overflow`和 断字`hyphenation`    
> - 文字阴影`text-shadow`和 文本修饰`text-decorations`    
> - 使用自定义字体`@font-face`      

* 新的展示性布局    
> 为了提高设计的灵活性，已经有两种新的布局被添加了进来:    
> - 多栏布局`column-count`、`column-width`    
> - 弹性布局`Flexible`    

### 8、硬件设备访问    

* [使用地理位置定位](https://developer.mozilla.org/zh-CN/docs/Web/Guide/HTML/HTML5)     
> HTML5 Geolocation API 用于获得用户的地理位置。    
> 鉴于该特性可能侵犯用户的隐私，除非用户同意，否则用户位置信息是不可用的。一般网页在调用此信息时，会弹出权限申请窗口。   

* [触控事件](https://developer.mozilla.org/zh-CN/docs/Web/API/Touch_events)    
> 对用户按下触控屏的事件做出反应的处理程序。   

* [检测设备方向](https://developer.mozilla.org/zh-CN/docs/Web/API/Detecting_device_orientation)     
> 让用户在运行浏览器的设备变更方向时能够得到信息。这可以被用作一种输入设备（例如制作能够对设备位置做出反应的游戏）或者使页面的布局跟屏幕的方向相适应（横向或纵向）。     

----------------
***参考资料***   
mnd： https://developer.mozilla.org/zh-CN/docs/Web/Guide/HTML/HTML5        
http://www.ganecheng.tech/blog/52819118.html       




