[TOC]



## 1. webpack介绍

本质上，*webpack* 是一个现代 JavaScript 应用程序的*静态模块打包器(module bundler)*。当 webpack 处理应用程序时，它会递归地构建一个*依赖关系图(dependency graph)*，其中包含应用程序需要的每个模块，然后将所有这些模块打包成一个或多个 *bundle*。

从webpack V4.0.0开始，可以不用引入一个配置文件，而webpack还是高度可配置的。

webpack的四个核心概念：

| 概念          | 作用                                                         |
| ------------- | ------------------------------------------------------------ |
| 入口(entry)   | 指示 webpack 应该使用哪个模块，来作为构建其内部*依赖图*的开始 |
| 输出(output)  | 告诉 webpack 在哪里输出它所创建的 *bundles*，以及如何命名这些文件 |
| loader        | 让 webpack 能够去处理那些非 JavaScript 文件（webpack 自身只理解 JavaScript） |
| 插件(plugins) | 执行范围更广的任务。插件的范围包括，从打包优化和压缩，一直到重新定义环境中的变量 |

一个简单的示例： 把编写的的代码转化为浏览器可以理解JS代码

```javascript
// src/index.js
import bar from './bar';
bar();

// src/bar.js
export default function bar() {
  //
}

// webpack.config.js 通过这个配置文件，执行后，可以生成浏览器理解的JS代码
const path = require('path');
module.exports = {
  entry: './src/index.js',
  output: {
      path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js'
  }
};
// page.html
<body>
    <script src="dist/bundle.js"></script>
</body>
```


## 2. entry(入口)、output(出口)

### 2.1 单个入口、出口写法

- 单个入口写法

  用法：`entry: string|Array<string>`

- 单个出口写法

  配置 `output` 属性的最低要求是，将它的值设置为一个对象，包括以下两点：

  1. `filename`: 用于输出的文件名
  2. `path`: 目标输出路径，绝对路径，也可以使用`path`模块来生成绝对路径

```javascript
const path = require('path');
const config = {
    // 入口
    entry: './path/to/my/entry/file.js',
    // 出口
    output: { filename: 'bundle.js',
       // path: '/home/proj/public/assets'
       path.join(__dirname,'../dist/')
    }
};
module.exports = config;
```



### 2.1 多个入口、出口写法

- 多个入口写法

  多个入口使用对象语法，用法：`entry: {[entryChunkName: string]: string|Array<string>}`

- 多个出口写法

  如果配置了多个入口，则应该使用[占位符(substitutions)](https://doc.webpack-china.org/configuration/output#output-filename)来确保每个文件具有唯一的名称。

```javascript
{
  entry: {
    app: './src/app.js',
    search: './src/search.js',
    pageOne: './src/pageOne/index.js',
    pageTwo: './src/pageTwo/index.js',
  },
  output: {
    filename: '[name].js',
    path: __dirname + '/dist' // __dirname 获取当前路径的绝对路径
  }
}
```



## 3. loader

loader 用于对模块的源代码进行转换。loader 可以使你在 `import` 或"加载"模块时预处理文件。

loader 可以将文件从不同的语言（如 TypeScript）转换为 JavaScript，或将内联图像转换为 data URL。loader 甚至允许你直接在 JavaScript 模块中 `import` CSS文件！

### 3.1 使用示例

如：让webpack加载CSS文件，或将TypeScript 转为 JavaScript。

首相安装相对应的loader：

```
npm install --save-dev css-loader
npm install --save-dev ts-loader
```

然后在配置文件`webpack.config.js`中配置，让webpack对每个`.css`使用`css-loader`,对所有`.ts`文件使用`ts-loader`:

```javascript
module.exports = {
  module: {
    rules: [
      { test: /\.css$/, use: 'css-loader' },
      { test: /\.ts$/, use: 'ts-loader' }
    ]
  }
};
```

### 3.2 使用loader的三种方式：配置、内联、CLI

#### 3.2.1 配置文件中配置

[`module.rules`](https://doc.webpack-china.org/configuration/module/#module-rules) 允许你在 webpack 配置中指定多个 loader。 这是展示 loader 的一种简明方式，并且有助于使代码变得简洁。同时让你对各个 loader 有个全局概览：

```javascript
  module: {
    rules: [
      {
        test: /\.css$/, use: [
          { loader: 'style-loader' }, 
          { loader: 'css-loader', options: { modules: true } }
        ]
      },
      { test: /\.scss$/, use: ['raw-loader', 'sass-loader'] },
    ]
  }
```

#### 3.2.2 内联：代码import语句后面使用

可以在 `import` 语句或任何[等效于 "import" 的方式](https://doc.webpack-china.org/api/module-methods)中指定 loader。使用 `!` 将资源中的 loader 分开。分开的每个部分都相对于当前目录解析。

```javascript
import Styles from 'style-loader!css-loader?modules!./styles.css';
```

通过前置所有规则及使用 `!`，可以对应覆盖到配置中的任意 loader。

选项可以传递查询参数，例如 `?key=value&foo=bar`，或者一个 JSON 对象，例如 `?{"key":"value","foo":"bar"}`。

#### 3.2.3 CLI:命令行中配置

```
webpack --module-bind jade-loader --module-bind 'css=style-loader!css-loader'
```

这会对 `.jade` 文件使用 `jade-loader`，对 `.css` 文件使用 [`style-loader`](https://doc.webpack-china.org/loaders/style-loader) 和 [`css-loader`](https://doc.webpack-china.org/loaders/css-loader)。

### 3.3 loader特性

- loader 支持链式传递。能够对资源使用流水线(pipeline)。一组链式的 loader 将按照相反的顺序执行。loader 链中的第一个 loader 返回值给下一个 loader。在最后一个 loader，返回 webpack 所预期的 JavaScript。
- loader 可以是同步的，也可以是异步的。
- loader 运行在 Node.js 中，并且能够执行任何可能的操作。
- loader 接收查询参数。用于对 loader 传递配置。
- loader 也能够使用 `options` 对象进行配置。
- 除了使用 `package.json` 常见的 `main` 属性，还可以将普通的 npm 模块导出为 loader，做法是在 `package.json` 里定义一个 `loader` 字段。
- 插件(plugin)可以为 loader 带来更多特性。
- loader 能够产生额外的任意文件。

loader 通过（loader）预处理函数，为 JavaScript 生态系统提供了更多能力。 用户现在可以更加灵活地引入细粒度逻辑，例如压缩、打包、语言翻译和[其他更多](https://doc.webpack-china.org/loaders)。

### 3.4 解析loader

loader 遵循标准的[模块解析](https://doc.webpack-china.org/concepts/module-resolution/)。多数情况下，loader 将从[模块路径](https://doc.webpack-china.org/concepts/module-resolution/#module-paths)（通常将模块路径认为是 `npm install`, `node_modules`）解析。

loader 模块需要导出为一个函数，并且使用 Node.js 兼容的 JavaScript 编写。通常使用 npm 进行管理，但是也可以将自定义 loader 作为应用程序中的文件。按照约定，loader 通常被命名为 `xxx-loader`（例如 `json-loader`）。有关详细信息，请查看[如何编写 loader？](https://doc.webpack-china.org/development/how-to-write-a-loader)。



## 4. 插件(Plugins)





该写插件了：

https://doc.webpack-china.org/concepts/plugins/





## webpack 中引入jQuery插件

1. 在项目中添加jQuery依赖：`npm install jquery --save-dev`

2. 在webpack配置文件的插件中添加如下代码：

   ```
   plugins: [
           new webpack.ProvidePlugin({ 
               $:"jquery", 
               jQuery:"jquery", 
               "window.jQuery":"jquery" 
           })
       ]
   ```

3. 直接在JS代码中使用：`var $ct = $(".img-ct");`

参考链接： https://yq.aliyun.com/ziliao/138017





## 参考资料

[webpack官网](https://webpack.js.org/)

[webpack中文官网](https://doc.webpack-china.org/)

[webpack概念](https://doc.webpack-china.org/concepts/)