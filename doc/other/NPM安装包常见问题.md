### 1. 使用淘宝源安装包出错

1. 使用npm安装`webpack`包的时候，发生了错误，

   ```
   npm install webpack --save-dev
   // 发生如下错误
   events.js:160░░░░░░⸩ ⠸ extract:repeat-string: sill extract remove-trailing-sepa
         throw er; // Unhandled 'error' event
         ^
   Error: write after end
       at writeAfterEnd (_stream_writable.js:193:12)
       at PassThrough.Writable.write (_stream_writable.js:240:5)
       at PassThrough.Writable.end (_stream_writable.js:477:10)
   ```

   后来查看安装源是淘宝的，换源可以解决这个问题：

   设置npmjs的源(可能需要VPN)，如果https不行就换成http的。

   ```
   // 查看安装源
   npm config get registry 	
   
   // 设置npm自己的源
   npm config set registry https://registry.npmjs.org/
   npm config set registry http://registry.npmjs.org/
   
   // 设置为淘宝源
   npm config set registry https://registry.npm.taobao.org/
   npm config set registry http://registry.npm.taobao.org/
   
   ```

   这个问题有的时候会发生，有时没问题，看人品了。

   还有一种情况，使用淘宝源： 使用公司网络安装失败，但是使用自己网络则安装成功。

2. 对于Error: write after end的另一个解决办法

   https://stackoverflow.com/questions/49148753/error-npm-err-write-after-end?rq=1

   文章里面大致的意思是降级npm版本：

   ```
   ~ npm -v
   6.1.0
   ~ npm install -g npm@5.6.0
   
   ~ npm -v
   5.6.0
   ```

   经过实测降级后错误没有了，但是又出现了另外一种错误：

   ```
   node-gyp rebuild
   
   xcode-select: error: tool 'xcodebuild' requires Xcode, but active developer directory '/Library/Developer/CommandLineTools' is a command line tools instance
   ```

   经过查找：

   https://github.com/nodejs/node-gyp/issues/569

   提示安装xcode-select：

   ```
   // 安装xcode-select  如果你没安装
   ~ xcode-select --install 
   // 验证是否安装成功
   ~ xcode-select -v
   xcode-select version 2349.
   // 启用命令行工具
   sudo xcode-select --switch /Library/Developer/CommandLineTools 
   ```

   我的项目问题没有解决，不过不影响我项目的运行

### 2. listen EADDRINUSE 服务端口被占用报错

```
npm start

> webpack-dev-server --config ./config/webpack.config.dev.js

events.js:160
      throw er; // Unhandled 'error' event
      ^
Error: listen EADDRINUSE 127.0.0.1:8080
    at Object.exports._errnoException (util.js:1018:11)
    at exports._exceptionWithHostPort (util.js:1041:20)
    at Server._listen2 (net.js:1258:14)
    at listen (net.js:1294:10)
```

当使用`npm start`启动一个web开发服务时，显示上面错误，经查找是端口(8080)被占用了。

解决方法：

1. 换一个端口，重新运行即可。
2. 找到被占用的端口，关掉占用的端口，重新运行即可。

```
// 查看是哪个进程占用的端口
~ sudo lsof -n -P | grep :8080

node      6534             dragon   14u     IPv4 0x3cf6bb332552824d        0t0        TCP 127.0.0.1:8080 (LISTEN)
// 关闭这个服务
kill -9 6534
```
