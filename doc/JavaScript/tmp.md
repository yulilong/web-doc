
## node 测试



```
console.log('1')
setTimeout(function() {
  console.log('2')
  new Promise(function(resolve) { console.log('4'); resolve(); })
  .then(function() { console.log('5') })
  setTimeout(() => { console.log('6') })
  new Promise(function(resolve) { console.log('7'); resolve()})
  .then(function() { console.log('8') })
})
setTimeout(function() { console.log('9') }, 0)
new Promise(function(resolve) { console.log('10'); resolve() })
.then(function() { console.log('11') })
setTimeout(function() {
  console.log('12')
  new Promise(function(resolve) { console.log('13'); resolve() })
  .then(function() {  console.log('14') })
})
new Promise(function(resolve) { console.log('15'); resolve() })
.then(function() { console.log('16') })

// node
// 1 10 15 2 4 7 9 11 12 13 16 5 6 8 14

// 浏览器
// 1 10 15 11 16 2 4 7 5 8 9 12 13 14 6
```

https://segmentfault.com/a/1190000012648569

https://segmentfault.com/a/1190000012362096



https://blog.csdn.net/i10630226/article/details/81369841

https://juejin.im/post/5af1413ef265da0b851cce80