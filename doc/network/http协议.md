

HTTP协议是服务器与浏览器之间传输数据的传送协议。

它可以使浏览器更加高效，使网络传输减少。它不仅保证计算机正确快速地传输超文本文档，还确定传输文档中的哪一部分，以及哪部分内容首先显示(如文本先于图形)等。

HTTP是一个应用层协议，由请求和响应构成，是一个标准的客户端服务器模型。HTTP是一个无状态的协议。



1. 首先客户端与服务器需要建立连接。只要单击某个超级链接，HTTP的工作开始。
2. 建立连接后，客户端发送一个请求给服务器，请求方式的格式为：统一资源标识符（URL）、协议版本号，后边是MIME信息包括请求修饰符、客户端信息和可能的内容。
3. 服务器接到请求后，给予相应的响应信息，其格式为一个状态行，包括信息的协议版本号、一个成功或错误的代码，后边是MIME信息包括服务器信息、实体信息和可能的内容。
4. 客户端接收服务器所返回的信息通过浏览器显示在用户的显示屏上，然后客户端与服务器断开连接。

如果在以上过程中的某一步出现错误，那么产生错误的信息将返回到客户端，有显示屏输出。对于用户来说，这些过程是由HTTP自己完成的，用户只要用鼠标点击，等待信息显示就可以了。

docsify主题：

https://jhildenbiddle.github.io/docsify-themeable/#/customization

## 参考资料



[http协议概念及其工作流程](https://blog.csdn.net/bv1315008634/article/details/53616584)

[http协议详解](https://www.cnblogs.com/wangning528/p/6388464.html)

说明了http发展史

[前端工程师，揭开HTTP的神秘面纱 segmentfault](https://segmentfault.com/a/1190000015493580)

对http的请求头、响应头介绍

[HTTP协议详解 segmentfault](https://segmentfault.com/a/1190000004457479)

[HTTP 协议入门 阮一峰](http://www.ruanyifeng.com/blog/2016/08/http.html)

