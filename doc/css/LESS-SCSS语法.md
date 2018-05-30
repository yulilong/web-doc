[TOC]

## 1. LESS

### 1.1 子代样式

正常的CSS写法： `.one > .son {}`

less写法：

```less
.one {
    > .son {color: red;}
}
```

### 1.2 :hover写法

正常CSS写法：`.one:hover`

less写法：

```less
.one {
    &:hover { color: red;}
}
```

### 1.3 后代样式

正常CSS写法：`.one .two{}`

less写法：

```less
.one {
    .two {}
}
```















## 参考资料

[LESS 快速使用指南 BOOTCSS](http://www.bootcss.com/p/lesscss/)

[快速入门 | Less.js 中文文档](https://less.bootcss.com/)