[TOC]

## 1. 创建一个仓库

可在网站创建好一个仓库后，clone到本地。

或者在本地新建一个目录，终端打开这个目录后：`git init`,然后添加一个远程仓库

## 2.  初始化一个package.json

终端中：`npm init -y`, 此命令执行结束后，会自动生成一个package.json文件



## 3. 安装vue-cli脚手架

```
$ npm install -g vue-cli
/usr/local/bin/vue -> /usr/local/lib/node_modules/vue-cli/bin/vue
/usr/local/bin/vue-init -> /usr/local/lib/node_modules/vue-cli/bin/vue-init
/usr/local/bin/vue-list -> /usr/local/lib/node_modules/vue-cli/bin/vue-list
+ vue-cli@2.9.3
added 6 packages from 2 contributors, removed 18 packages and updated 43 packages in 14.47s

~ vue -V
2.9.3
```

注意：此文档使用的vue-cli版本是`2.9.3`.

## 4. vue init webpack:通过webpack来创建一个项目

应为上面已经创建目录了，所以直接在这个目录中构建一个项目：

```
vue init webpack .
// 注意上面的点不能忽略，表示直接在当前目录构建项目。

? Generate project in current directory? (Y/n) 是否在当前目录生成 回车就好
downloading template

? Project name (vue-init)	项目名称 默认回车就好

? Project description (A Vue.js project) 项目描述 默认回车就好

? Author (user <user@outlook.com>)	作者	默认回车就好

? Vue build (Use arrow keys)
❯ Runtime + Compiler: recommended for most users
  Runtime-only: about 6KB lighter min+gzip, but templates 
  (or any Vue-specific HTML) are ONLY allowed in .vue files 
  - render functions are required elsewhere
  这个是要问使用哪一个版本的vue： 运行时 + 编译 ， 仅运行时
  键盘上下键选择， 我们选择第一个：开发时用，选好后 回车
  
? Install vue-router? (Y/n)	 是否安装 vue路由 回车安装

? Use ESLint to lint your code? (Y/n)	是否使用ESLint来检查代码语法 n
❯ Standard (https://github.com/standard/standard)
  Airbnb (https://github.com/airbnb/javascript)
  none (configure it yourself)
  
? Set up unit tests (Y/n)	设置单元测试？ n

? Setup e2e tests with Nightwatch? (Y/n)	设置端到端测试？ n

? Should we run `npm install` for you after the project has been created? (recommended) (Use arrow keys)
❯ Yes, use NPM
  Yes, use Yarn
  No, I will handle that myself
  项目创建完成后，我们是否应该为你运行`npm install`？
  
vue-cli · Generated "vue-init".

# Installing project dependencies ...
# ========================
```

[vue 对不同构建版本的解释](https://cn.vuejs.org/v2/guide/installation.html#%E5%AF%B9%E4%B8%8D%E5%90%8C%E6%9E%84%E5%BB%BA%E7%89%88%E6%9C%AC%E7%9A%84%E8%A7%A3%E9%87%8A)



也可以使用该命令从一个新目录中构建：

```
~ vue init webpack my-project

? Project name my-project
? Project description A Vue.js project
? Author user <user@outlook.com>
? Vue build standalone
? Install vue-router? Yes
? Use ESLint to lint your code? Yes
? Pick an ESLint preset Standard
? Set up unit tests No
? Setup e2e tests with Nightwatch? No
? Should we run `npm install` for you after the project has been created? (recom
mended) no

   vue-cli · Generated "my-project".

// Project initialization finished!
// ========================

To get started:

  cd my-project
  npm install (or if using yarn: yarn)
  npm run lint -- --fix (or for yarn: yarn run lint --fix)
  npm run dev

Documentation can be found at https://vuejs-templates.github.io/webpack

```

## 5. 打开项目安装依赖运行

使用vue-cli创建好一个项目后打开项目，运行`npm install`安装依赖包，依赖包装好后即可启动项目：

```
npm install 	// 安装依赖包

npm start		// 启动服务
```

## 6. 设置支持scss、less

### 6.1 安装less、scss依赖

```
~ npm install less less-loader --save-dev	// 安装 less依赖
+ less@3.0.4
+ less-loader@4.1.0
added 39 packages from 67 contributors in 21.585s

// 安装sass的依赖包, sass-loader依赖于node-sass
~ npm install sass-loader node-sass --save-dev
+ sass-loader@7.0.1
+ node-sass@4.9.0
added 85 packages from 88 contributors in 52.185s
```

### 6.2 在webpack配置文件中配置

如果是通过vue-cli来构建的项目，那么vue-cli已经帮我们配置好了，只不过没有安装依赖包。

在webpack.dev.conf.js中，我们可以看到下面的代码：

```
// 2018-05-22
module: {
    rules: utils.styleLoaders({ sourceMap: config.dev.cssSourceMap, usePostCSS: true })
  },
```

即webpack.dev.conf.js在合并了webpack.base.conf.js的基础上又添加了dev环境下的module。

在build文件夹下有一个utils.js文件，这个文件提供了一些通用的方法，供webpack.dev.conf.js和webpack.prod.conf.js使用。 其中styleLoaders方法如下：

```
// Generate loaders for standalone style files (outside of .vue)
exports.styleLoaders = function (options) {
  const output = []
  const loaders = exports.cssLoaders(options)
  for (const extension in loaders) {
    const loader = loaders[extension]
    output.push({
      test: new RegExp('\\.' + extension + '$'),
      use: loader
    })
  }
  return output
}
```

通过这个方法可以对大多数css预处理进行了配置，具体配置在cssLoaders方法中。



### 6.3 scss、less在文件用使用

在`app.vue`文件中的用法

```html
<template>
  <div id="app"> <p>nihao <span>123</span></p> </div>
</template>
<script>
    // 也可以在这里引入外部文件
    import './assets/less/abc.less';	
    import './assets/scss/abc.scss';
</script>
<!-- less -->
<style lang="less" scoped>
#app {
  p {
    color: red; font-size: 20px;
    &:hover {color: blue;}  span { color: green; }
  }
}
</style>
<!-- scss用法 -->
<style lang="scss" scoped>
</style>
```

需要注意一下几点：

1. 已经在webpack中配置了，所以这里不需要引入任何less文件。
2. 在style中声明lang="less"。 注意： scoped的作用仅仅是限定css的作用域，防止变量污染。
3. 这样就可以根据less的语法使用了。

注意，加了scoped后生成的样式的文件：

```html
<p data-v-7ba5bd90="">nihao <span data-v-7ba5bd90="">123</span></p>
<!-- 如果没加scoped 则没有data-v-7ba5bd90  --->
```





## 参考资料

[vue-cli构建项目使用 less](http://www.cnblogs.com/zhuzhenwei918/p/6870340.html)

