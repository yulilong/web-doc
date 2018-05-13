Google浏览器开发者工具使用：

1. 模拟手机查看网页，

   打开开发者工具 -> 左上角Toggle device toolbar，点击一下按钮。

   就可以以手机形式浏览网页，在此页面的右上角有三个点，点击可出现一个菜单，选择`Add device type`可以选择设备类型，在出现的选项里可以选择实在手机浏览还是在桌面端浏览。

   ​

## 手机端页面的做法

1. 学会 media query
2. 学会要设计图（没图不做）
   1. 实在要做也行，丑可别怪我
3. 学会隐藏元素
4. 手机端要加一个 meta
   `<meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">`
5. 手机端的交互方式不一样
   1. 没有 hover
   2. 有 touch 事件
   3. 没有 resize
   4. 没有滚动条



## media query

[CSS媒体查询mdn](https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Media_queries) 

[w3c媒体查询](https://www.w3cschool.cn/cssref/css3-pr-mediaquery.html)

media满足CSS3规范的条件下，包含零个或多个表达式，这些表达式描述了媒体特征，最终会被解析为true或false。

```html
<!-- link元素中的CSS媒体查询 -->
<link rel="stylesheet" media="(max-width: 800px)" href="example.css" />
<!-- 样式表中的CSS媒体查询 -->
<style>
/*@media (min-width: 320px) and (max-width: 480px) */
@media (max-width: 600px) {
  .nav { display: none; }
}
</style>
```

当媒体查询为true时，才会应用样式。当媒体查询为false是，`<link>` 标签指向的样式表也会加载，但不会应用。

其中：   

- `max-width: 600px`: 表示显示宽度0~600px都符合条件
- `min-width: 320px`:表示显示宽度大于等于320像素都符合条件，0~319px不符合条件。
- `(min-width: 320px) and (max-width: 480px)`：表示显示宽度大于等于320px并且小于等于480px才符合条件。



## 使用服务来启动一个本地html

- 安装一个服务，这个服务用来启动本地HTML服务

  ```
  ~ npm i -g http-server

  /usr/local/bin/http-server -> /usr/local/lib/node_modules/http-server/bin/http-server
  /usr/local/bin/hs -> /usr/local/lib/node_modules/http-server/bin/http-server
  + http-server@0.11.1
  updated 3 packages in 8.379s
  ```

- 本地创建一个项目目录，里面新建一个HTML文件，写好代码后保存，终端打开这个项目目录，运行下面命令启动服务：

  ```
  ~ http-server -c-1

  Starting up http-server, serving ./
  Available on:
    http://127.0.0.1:8080
    http://192.168.43.176:8080
  Hit CTRL-C to stop the server
  ```

- 此时就可以在浏览器中输入`http://127.0.0.1:8080`来访问页面。



## 使用媒体查询来做手机适配

使用媒体查询来判断手机屏幕大小，根据屏幕大小的不同来做不同的布局。

```html
<style>
  	@media (max-width: 425px) {
  		body { background: green; }
  	}
  	@media (max-width: 375px) {
  		body { background: orange; }
  	}	
  	@media (max-width: 320px) {
  		body { background: red; }
  	}
</style>
<div>hello world</div
```

根据选择器的优先级，优先级相同后面覆盖前面的，上面的样式就可以做到根据屏幕宽度的不同显示不同的背景色。

还可以把条件写的更严格一些，这样宽度不同就只能应用一种样式了。

```html
<style>
  	@media (min-width: 376px) and (max-width: 425px) {
  		body { background: green; }
  	}
  	@media (min-width: 321px) and (max-width: 375px) {
  		body { background: orange; }
  	}	
  	@media (max-width: 320px) {
  		body { background: red; }
  	}
</style>
<div>hello world</div
```


国外一个响应式的网站：https://www.smashingmagazine.com/     



## 响应式先做手机端还是先做PC端：

根据不同的显示设备对应做出不同的样式显示，

### 先做手机端叫：mobile first

http://getbootstrap.com/ 在bootstrap官网上就出现了mobile first 这个词，就是表示手机端开发优先。

推荐手机端有线开发，因为手机端用户多。

### 先做PC端叫：desktop first



## 菜单显示与隐藏按钮实现响应式



```html
<button id="menu">菜单</button>
<div id="nav">
    <span>标题1</span>
    <span>标题2</span>
    <span>标题3</span>
</div>
<script>
    menu.onclick = function() {
        if (nav.style.display === 'block'){
            nav.style.display = 'none'
        } else {
            nav.style.display = 'block'
        }
    }
</script>
```

这样当点击菜单按钮就会实现菜单的显示与隐藏，但这样不好，最好使用JS去切换样式：

```html
<style>
    #nav.active { display: none;}
</style>
<button id="menu">菜单</button>
<div id="nav">
    <span>标题1</span>
    <span>标题2</span>
    <span>标题3</span>
</div>
<script>
    menu.onclick = function() {
        nav.classList.toggle('active')
    }
</script>
```

这样JS操作的就是CSS类，



## 淘宝、京东网站等网站手机端web跟PC端web是分开的两套网页

他们的网站 手机访问跟PC电脑访问页面的网站不是同一个。手机一个网站、PC端一个网站

## 真正响应式网站是很少的

如果做响应式，代码是很多了，需要做两套代码， 一般只有新闻类网站才是响应式的，因为简单、不复杂。



## meta viewport 禁止设置缩放，解决手机端页面自动缩小页面

历史原因：

最开始web都是给PC端看的， 诺基亚出来后，他有自己的专门语言来编写手机web，当iPhone出来的时候，手机看网页时，是把页面缩放(缩放比例：模拟980px，全世界网站页面宽度在980px左右)，把手机屏幕模拟成电脑端的宽度，当用户想要看内容的时候，自己点击屏幕放大页面浏览.

在chrome浏览器中，打开开发者工具，选择手机端，然后再控制台中输入：

```javascript
document.documentElement.clientWidth
980
```

就可以看见手机浏览器模拟了980px的屏幕宽度。可在HTML代码中放入如下代码，即可阻止浏览器缩放：

```html
<!-- meta:vp 然后按tab键，即可出来-->
<meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
```

viewport 视口， 宽度等于设备宽度， 用户缩放：禁止， 初始缩放倍数： 1.0， 最大缩放倍数： 1.0，最小缩放倍数： 1.0



##  手机端特点

1. 没有 hover

2. 有 touch 事件

   两次touch事件，记录两次触摸的位置就可以知道向哪边滑动，有现成的封装库，jQuery .swipe,

   不要去监听click事件很少，一般都是滑动事件

3. 没有 resize

   无法调整屏幕大小， 浏览器的宽度等于设备宽度。

4. 没有滚动条

   手机上会把网页的滚动条隐藏，只有在滑动的时候才会出现，只是做一个提示用。

   外观差异巨大。

5. 手机跟PC CSS基本没有区别

6. 手机上没有IE浏览器，能用最新就用最新的技术。

