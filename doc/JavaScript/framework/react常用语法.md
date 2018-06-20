[TOC]

### 1. react样式的写法

- JSX中使用样式 

  1、行内样式：写行内样式的时候需要使用两个{}  ==>{{}}    

   2、对象样式：在return前面定义一个样式对象，注意样式的写法，与HTML的不同点     

  3、CSS样式

- 在HTML5中与在React中的样式的书写区别

  1、HTML5中以;结束          

  ​	在React中以,结束

   2、在HTML5中属性与值都不需要加上引号          

  ​	在React中，属于javascript对象，key中不能存在 - ,需要使用驼峰命名，如果是value值，需要加上引号

  3、在HTML中，设置带数字的值，宽度，高度==，需要带上单位

  ​         在React中可以不用带单位，直接写数字 这里是指那些规定了默认单位的值。比如说像素px，如果要使用em或者是rem则需要加上单位

- 其他注意事项

  {} 插值符号 (例如写行内style样式的时候为啥要用{{}})      

  在使用插值符号的时候，里面需要时一个对象或者是一个表达式

```jsx
var HelloWorld = React.createClass({  
    render:function(){  
        var styles = {   color: 'blue',  fontSize: '30'  }  
        return (  
            <div className="box">  
                <h3 className="title" 
                  style={{color:'red',backgroundColor:'lime'}}>默认标题</h3>  
                <p className="subtitle" style={styles}>说明</p>  
                <p className="details">这个是用来教学的案例</p>  
            </div>  
        )  
    }  
})  
ReactDOM.render(<HelloWorld/>,document.getElementById("app"))  
```

参考资料：https://blog.csdn.net/chuipaopao163/article/details/73432229

### 2. 生命周期（Lifecycle）

React 的生命周期包括三个阶段：mount（挂载）、update（更新）和 unmount（移除）

#### 2.1 mount

mount 就是第一次让组件出现在页面中的过程。这个过程的关键就是 render 方法。React 会将 render 的返回值（一般是虚拟 DOM，也可以是 DOM 或者 null）插入到页面中。

这个过程会暴露几个钩子（hook）方便你往里面加代码：

1. constructor()
2. componentWillMount()
3. render()
4. componentDidMount()

我用一幅图解释一下：

![](http://cdn.jscode.me/2017-04-09-14916683117874.jpg)

#### 2.2 update

mount 之后，如果数据有任何变动，就会来到 update 过程，这个过程有 5 个钩子：

1. componentWillReceiveProps(nextProps) - 我要读取 props 啦！

2. shouldComponentUpdate(nextProps, nextState) - 请问要不要更新组件？true / false
3. componentWillUpdate() - 我要更新组件啦！
4. render() - 更新！
5. componentDidUpdate() - 更新完毕啦！

 #### 2.3 unmount

当一个组件将要从页面中移除时，会进入 unmount 过程，这个过程就一个钩子：

1. componentWillUnmount() - 我要死啦！

你可以在这个组件死之前做一些清理工作。

 