## 原则

- 不到万不得已，不要写死 width 和 height
- 尽量用高级语法，如 calc、flex
- 如果是 IE，就全部写死
- 布局的div只用来做布局，内容新建一个div去写

## 布局方式

- 需要兼容IE8：

float布局： 定宽



- 不需要兼容IE8：

flex布局：弹性宽度



### float布局

1. 给子元素加：`float: left`或`float:right`
2. 父元素清除浮动：`clearfix`
3. 如果宽度不够，可以用 margin: 0 -4px;   

```
.clearfix:after{
    content: '';
    display: block;
    clear: both;
}
.clearfix{
    zoom: 1;
}
```

### flex布局

1. 父元素加`display:flex`
2. 父元素加`justify-content: space-between;`
3. 如果宽度不够，可以用 margin: 0 -4px;  

## 写一个页面

pc端：

```
+-------------------------------------------------------+
|                                                       |
| +--------+                 +----+ +----+ +---+ +----+ |
| | logo   |                 | 菜单| |菜单| |菜单| |菜单 | |
| +--------+                 +----+ +----+ +---+ +----+ |
|   +-----------------------------------------------+   |
|   |                                               |   |
|   |        banner                                 |   |
|   |                                               |   |
|   |                                               |   |
|   |                                               |   |
|   +-----------------------------------------------+   |
|                                                       |
|   +--------+  +---------+  +---------+  +---------+   |
|   |        |  |         |  |         |  |         |   |
|   |        |  |         |  |         |  |         |   |
|   +--------+  +---------+  +---------+  +---------+   |
|   +--------+  +---------+  +---------+  +---------+   |
|   |        |  |         |  |         |  |         |   |
|   +--------+  +---------+  +---------+  +---------+   |
|                                                       |
|   +------------+  +-------------------------------+   |
|   |            |  |                               |   |
|   |            |  |                               |   |
|   |            |  |                               |   |
|   |            |  |                               |   |
|   |            |  |                               |   |
|   |            |  |                               |   |
|   |            |  |                               |   |
|   |            |  |                               |   |
|   |            |  |                               |   |
|   +------------+  +-------------------------------+   |
|                                                       |
+-------------------------------------------------------+

```

手机端：

```
+-----------------------------+
| +--------+           +----+ |
| |        |           |----| |
| +--------+           +----+ |
| +-------------------------+ |
| |                         | |
| |                         | |
| |                         | |
| +-------------------------+ |
|  +--------+  +----------+   |
|  |        |  |          |   |
|  |        |  |          |   |
|  +--------+  +----------+   |
|  +--------+  +----------+   |
|  |        |  |          |   |
|  +--------+  +----------+   |
|  +--------+  +----------+   |
|  |        |  |          |   |
|  +--------+  +----------+   |
+-----------------------------+
```



## 桌面布局



```html
<body>
  <style>
    * {box-sizing: border-box;}
    .clearfix:after{content: ''; display: block; clear:both;}
    .clearfix {zoom: 1;} /*IE6*/
    
    .parent {border: 1px solid; padding: 5px;
      background: #ddd; text-align: center; min-width: 600px;
    }
    .logo {border: 1px solid;
      background: black; color: white; width: 70px;
      line-height: 36px;
    }
    .menu > div {border: 1px solid; 
      line-height: 36px; margin-left: 10px;}
    
    .banner {
      border: 1px solid; width: 600px; height: 200px;
      margin: 10px auto 0 auto; background: #ccc;
    }
    .pictures { width: 600px; margin: 10px auto 0 auto; }
    .middle { margin: 0 -20px; }
    .picture {
      width: 120px; height: 80px;  background: red;
      border: 1px solid;
    }
    
    /*使用float布局*/
    /* .pic-float { float: left; margin: 20px; } */
    
    /*使用flex布局，这种如果一行有三个，那么也是左对齐*/
    .pictures-flex { display: flex; flex-wrap: wrap; }
    .pic-flex { margin: 15px; width: calc(25% - 30px); margin-bottom: 10px; }
    .middle { margin: 0 -15px; }
    
    /*使用flex布局，这种的一行必须4个， 否则会两边对齐，*/
    /* .pictures-flex {
      display: flex; flex-wrap: wrap; justify-content: space-between;
    }
    .pic-flex { width: 130px; margin-bottom: 10px; } 
    .middle { margin: 0; } */
    /*广告*/
    .art { border: 1px solid; margin: 0 auto; width: 600px; }
    .one {
      height: 200px; border: 1px solid; background: #aaa;
      width: calc(33.3% - 20px); margin-right: 20px;
    }
    .two {
      height: 200px; border: 1px solid; background: #eee; width: 66.66%;
    }
    /*使用float布局*/
     /* .art >div { float: left; } */
    /*使用flex布局*/
    .art { display: flex; }
  </style>
  <div class="parent clearfix">
    <div class="logo" style="float: left">logo</div>
    <div class="menu clearfix"style="float: right">
      <div style="float: left">菜单1</div>
      <div style="float: left">菜单2</div>
      <div style="float: left">菜单3</div>
      <div style="float: left">菜单4</div>
      <div style="float: left">菜单5</div>
    </div>
  </div>
  <div class="banner"></div>
  
  <div class="pictures clearfix">
    <div class="middle  pictures-flex">
      <div class="picture pic-float pic-flex"></div>
      <div class="picture pic-float pic-flex"></div>
      <div class="picture pic-float pic-flex"></div>
      <div class="picture pic-float pic-flex"></div>
      <div class="picture pic-float pic-flex"></div>
      <div class="picture pic-float pic-flex"></div>
      <div class="picture pic-float pic-flex"></div>
      <!-- <div class="picture pic-float pic-flex"></div> -->
    </div>
  </div>
  <div class="art clearfix">
    <div class="one">广告1</div>
    <div class="two">广告2</div>
  </div>
</body>
```

add不能作为CSS类名， 因为很有可能被广告屏蔽软件屏蔽。



## 手机布局

代码在上面的基础上加了一些，

- CSS样式加载上面代码的后面，这样当切换手机浏览时，后面的样式覆盖前面，就应用手机布局。
- 上面的菜单加了一个按钮，当手机上浏览时，PC上的菜单影藏，改成按钮显示。

```html
<style>
    .parent .menu2 {display: none;}
    @media (max-width: 420px) {
      * {margin: 0; padding: 0;}
      .parent {min-width: auto;}
      .parent .menu {display: none;}
      .parent .menu2 {display: block;}
      .banner {width: auto;}
       /*这里使用overflow是因为图片的div宽度大于屏幕宽度了，所以加上了hidden*/
      .pictures { width: auto; overflow: hidden;}
      .pic-flex { width: calc(50% - 30px);}
      .art { width: auto; flex-direction: column;}
      .one,.two { width: auto; margin: 0;}
    }
  </style>
<div class="menu2">三</div>
<!-- http://js.jirengu.com/qucof/12/edit?html,output -->
```



布局切换的时候，宽度变化的时候，想要图片不变形，那么久不要用img标签。使用 背景图片。

```css
div {
    background: transparent url(https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=3591147451,1203661331&fm=27&gp=0.jpg) no-repeat center;
      background-size: cover;
}
```



如果非要全显示搜索固定比例div