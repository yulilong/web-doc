[TOC]

## 1. 垂直水平居中

### 1.1 高度固定，

```html
<style>
    .location { height: 360px; width: 100%; border: 1px solid; text-align: center; }
    .location::before {
        content: '';
        display: inline-block;
        height: 100%;
        vertical-align: middle;
    }
    .location .center {
        display: inline-block;
        vertical-align: middle;
    }
    .location .word-zh {
        font-size: 32px;
    }
    .location .word-en {
        font-size: 24px;
    }
</style>
<div class="location">
    <div class="center">
        <div class="word-zh">你好</div>
        <div class="word-en">哈哈</div>
    </div>
</div>
```



### 垂直居中

2018-01-21直播

### 居中vs不居中
[代码](http://js.jirengu.com/feki/1/edit?html,css,output)

### 绝对定位实现居中
[代码](http://js.jirengu.com/wuxa/1/edit)

```
<body>
  <div class="dialog">
    <div class="header">我是标题</div>
    <div class="content">我是内容</div>
  </div>
</body>
/*yi*/
.dialog {
  position: absolute;
  left: 50%;
  top: 50%;
  margin-left: -200px;
  margin-top: -150px;
  
  width: 400px;
  height: 300px;
  box-shadow: 0px 0px 3px #000;
}

/*er*/
.dialog {
  position: absolute;
  left: calc(50% - 200px);
  top: calc(50% - 150px);
  width: 400px;
  height: 300px;
  box-shadow: 0px 0px 3px #000;
}
```


### 应用场景   



### vertical-align实现居中
[代码](http://js.jirengu.com/rafu/1/edit)

vertical-align: middle; 只对行内元素和表格元素生效。

### table-cell实现居中
[代码](http://js.jirengu.com/nape/1/edit)
