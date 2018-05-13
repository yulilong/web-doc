## nodejs安装

[官网下载](https://nodejs.org/en/download/)

选择对应的操作系统，然后点击安装。[安装教程](http://www.runoob.com/nodejs/nodejs-install-setup.html) 

安装好后在终端查看node版本，如果出现版本了，那么表示安装成功：

```
~ node -v
v6.11.1
```

使用nodejs运行程序：

```
node server.js
```

## 1、运行一个最简单服务器

1. 创建一个目录，在目录里面创建一个文件：

   node-server/server.js

   ```javascript
   var http = require('http')
   var server = http.createServer(function(req, res){
     res.write('hello')
     res.end()
   })
   console.log('open http://localhost:3000')
   server.listen(3000)
   ```

2. 终端打开node-server目录，运行如下命令：

   ```
   node server.js 
   open http://localhost:3000
   ```

3. 在浏览器中输入`http://localhost:3000`就可以看见效果。



## 2、让nodeJS像Nginx一样读取服务器上静态页面

1. 编写nodeJS代码：node-server/server.js

   ```javascript
   var http = require('http')
   var url = require('url')        // 对URL解析的一个包
   var path = require('path')      // 自动处理各系统路径的包
   var fs = require('fs')          // 读取文件的包

   function loadWeb(filePath, req, res){
     var urlObj = url.parse(req.url)		// 解析url
     // 如果没有输入路径，默认返回index.html内容
     if (urlObj.pathname === '/') {
       urlObj.pathname += 'index.html'
     }
     var webPath = path.join(filePath, urlObj.pathname)	// 定位要请求的文件
     // 读取文件(文件路径， 二进制读取， 读取后处理方式(错误，读取的内容))
     fs.readFile(webPath, 'binary', function(err, fileContent){
       if (err) {
         res.writeHead(404, 'page not found')
         res.end('<h1>404, the page is not found</h1>')
       } else {
         res.writeHead(200, 'OK')
         res.write(fileContent, 'binary')
         res.end()
       }
     }) 
   }
   var server = http.createServer(function(req, res){
     loadWeb(path.join(__dirname, 'dist'), req, res)
   })
   console.log('open http://localhost:3000')
   server.listen(3000)
   ```

   **注：**变量`__dirname`是获取当前文件的路径，是nodeJS的全局变量,详情参考：[Node.js 全局对象](http://www.runoob.com/nodejs/nodejs-global-object.html)

   ​

2. 项目中创建一个简单的网页：

   node-server/dist/index.html

   ```html
   <!DOCTYPE html> <html lang="en">
   <head>
   	<meta charset="UTF-8"> <title>Document</title>
   	<link rel="stylesheet" href="css/style.css">
   </head>
   <body> <h1>我是测试文件</h1> </body>
   </html>
   ```

   node-server/dist/css/style.css

   ```css
   h1 { color: red; border: 1px solid green;}
   ```

3. 终端打开项目，运行`node server.js `，启动服务，

4. 在浏览器中输入`http://localhost:3000`就可以看见页面了。

## 3、编写一个API

1. node-server/server.js

   根据路径的不同做相应的处理。

   ```javascript
   var http = require('http')
   var url = require('url')        // 对URL解析的一个包

   var server = http.createServer(function(req, res){
     res.setHeader('Access-Control-Allow-Origin','*')	// 允许任何页面访问接口
     var urlObj = url.parse(req.url);
     switch (urlObj.pathname) {
       case '/getInfo':
         res.writeHead(200, 'OK')
         res.write('I am base info');
         break;
       case '/show':
         res.writeHead(200, 'OK')
         res.write('Show somethings');
         break;
       default:
         res.writeHead(404, 'page not found')
         res.end('<h1>404, the page is not found</h1>')
     }
     res.end()
   })
   console.log('open http://localhost:3000')
   server.listen(3000)
   ```

2. 在浏览器开发者的console中运行如下代码：

   ```javascript
   var xhr = new XMLHttpRequest()
   xhr.open('GET', 'http://localhost:3000/getInfo', true)
   xhr.onreadystatechange = function(){
       if(xhr.readyState === 4) {
           console.log(xhr.responseText)
       }
   }
   xhr.send()
   ```

   或者有Chrome浏览器插件Postman中测试。就能看见效果。

## 4、 API的get、post方法

[Node.js GET/POST请求 菜鸟教程](http://www.runoob.com/nodejs/node-js-get-post.html)

node-server/server.js

根据`method`方法来判断是get还是post方法， 

```javascript
var http = require('http')
var url = require('url')        // 对URL解析的一个包
var querystring = require('querystring'); // 解析POST的参数

var server = http.createServer(function (req, res) {
  res.setHeader('Access-Control-Allow-Origin','*')	//允许跨域
  var urlObj = url.parse(req.url);
  switch (urlObj.pathname) {
    case '/getInfo':
      res.writeHead(200, 'OK')
      if (req.method.toUpperCase() === 'GET') {
        res.write('I am base info GET,  GET'); res.end();
      } else if (req.method.toUpperCase() === 'POST') {
        res.write('I am POST');
        var body = "";
        req.on('data', function (chunk) { body += chunk; });
        req.on('end', function () {
          body = querystring.parse(body); // 解析参数
          if (JSON.stringify(body) !== "{}"){ res.write(body.info); }
          res.end();
        });
      }
      break;
    default:
      res.writeHead(404, 'page not found')
      res.write('<h1>404, the page is not found</h1>')
      res.end();
  }
})
console.log('open http://localhost:3000')
server.listen(3000);
```

**注：**`res.end();`只能执行一次，多次执行就报错，并让nodeJS程序退出， 关闭后不能在写`res.write`, 否则也报错。

在浏览器开发者的console中运行如下代码：

```javascript
var xhr = new XMLHttpRequest()
xhr.open('post', 'http://localhost:3000/getInfo', true)
xhr.onreadystatechange = function(){
    if(xhr.readyState === 4) { console.log(xhr.responseText) }
}
var info = "info={'FullName':'小明','Company':'母鸡'}";
xhr.send(info)
// 返回的结果
// I am POST{'FullName':'小明','Company':'母鸡'}
```





## 参考



[nodeJS官网文档](https://nodejs.org/en/docs/)

[nodejs中http模块文档](https://nodejs.org/dist/latest-v8.x/docs/api/http.html)

[Node.js 教程 菜鸟教程](http://www.runoob.com/nodejs/nodejs-tutorial.html)



