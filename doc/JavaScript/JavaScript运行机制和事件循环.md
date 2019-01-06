## 1. JavaScript是单线程执行的

JavaScript语言的执行是单线程(single thread)的。

所谓的`单线程`，就是指一次只执行一个任务，如果有多个任务，就必须排队，前面一个任务完成，才能执行后面任务。

这种模式的好处是实现起来比较简单，执行环境相对单纯；坏处是只要有一个任务耗时很长，后面的任务都必须排队等待，会拖延整个程序的执行。常见的浏览器无响应(假死)，往往就是因为某一段JavaScript代码长时间运行(比如死循环)，导致整个页面卡在这个地方，其他任务无法执行。

为了解决这个问题，JavaScript语言将任务的执行模式分成两种：`同步(Synchronous)`和`异步(Asynchronous)`。

`同步任务`：在主线程上排队执行的任务，只有前一个任务执行完毕，才能执行后一个任务。

`异步任务`：不进入主线程、而进入"任务队列"（task queue）的任务，只有"任务队列"通知主线程，某个异步任务可以执行了，该任务才会进入主线程执行。

JavaScript执行机制：

> 1. 所有同步任务都在主线程上执行，形成一个执行栈（execution context stack）。
> 2. 主线程之外，还存在一个"任务队列"（task queue）。只要异步任务有了运行结果，就在"任务队列"之中放置一个事件。
> 3. 一旦"执行栈"中的所有同步任务执行完毕，系统就会读取"任务队列"，如果有有执行任务，则进入执行栈，开始执行。
> 4. 主线程不断重复上面的三步，此过程也就是常说的Event Loop(事件循环)。









## 参考资料



`https://mp.weixin.qq.com/s?__biz=MzA5NzkwNDk3MQ==&mid=2650585345&amp;idx=1&amp;sn=6fd112fbed64246601b48e392d1e7a0b&source=41#wechat_redirect`

http://www.yangzicong.com/article/3

http://www.ruanyifeng.com/blog/2014/10/event-loop.html

https://segmentfault.com/a/1190000012362096

https://segmentfault.com/a/1190000017120344#articleHeader8