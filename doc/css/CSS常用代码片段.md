[TOC]

### 1. 高度自适应屏幕高度

例子： 网站底部的版权条，当内容不足一屏的时候显示在屏幕的底部，在内容超过一屏的时候显示在所有内容的底部。

使用flex布局：

```html
<style>
    .container { display: flex; min-height: 100vh;
        flex-direction: column;
    }
    header { background: #cecece; min-height: 100px;
    }
    content { background: #bbbbbb;
        flex: 1; /* 1 代表盡可能最大，會自動填滿除了 header footer 以外的空間 */
    }
    footer { background: #333333; min-height: 100px; }
</style>
<div class="container">
  <header></header>
  <content></content>
  <footer></footer>
</div>
```

这样`<footer>`就会在底部了。

参考资料：https://blog.csdn.net/u014374031/article/details/69258208