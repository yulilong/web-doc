[TOC]

# Transitions、Transforms和Animation

这三个属性都是CSS3版本的属性，所以会有兼容性问题。

## 1. Transitions

- transition-property

  过渡的属性的名称，比如 transition-property:backgrond 就是指 backgound 参与这个过渡

- transition-duration

  定义过渡效果花费的时间,默认是 0

- transition-timing-function

  规定过渡效果的时间曲线,用于指定过渡类型，有 ease | linear | ease-in | ease-out | ease-in-out | cubic-bezier

  linear(匀速) ease(慢速开始，然后变快，然后慢速结束)

- transition-delay

  规定过渡效果何时开始。默认是 0。用于制定延迟过渡的时间

当然，一般情况下，我们都是写一起的，比如：`transition： width 2s ease 1s` 。

```
transition: transition-property transition-duration transition-delay
```

```less
.box {
  width: 100px;
  height: 100px;
  background: red;
  transition: width 2s;
  -weikit-transition: width 2s; /* Safari*/
}
.box:hover {
  width: 400px;
}
```

上面的代码在鼠标放入后div的宽会在2秒内变宽到400px。

[在线代码](http://js.jirengu.com/xadub/1/edit)

## 2. Transforms

指拉伸，压缩，旋转，偏移等等一些图形学里面的基本变换。

`skew`是倾斜，`scale`是缩放，`rotate`是旋转，`translate`是平移。最后需要说明一点，transform 支持综合变换。

### 2.1 旋转:rotate

```html
<style>
    .one {
        width: 200px;
        height: 200px;
        background-color: red;
        transition: transform 1s linear;
    }
    .one:hover {
        transform: rotate(-180deg);
    }
</style>
<div class="one"></div>
```



## 3. Animation





## 参考资料



1. [CSS3动画相关属性详解 CSDN](https://blog.csdn.net/lyznice/article/details/54575905)
