## 1. 函数介绍

### 1.1 函数的三种声明

```javascript
// function命令
function p(s) {console.log(s)};
// 函数表达式
var p = function(s) {console.log(s)};
// 调用执行函数
p('sssssss')	// ssssss
// Function构造函数
var add = new Function('x', 'y', 'return x + y')
// 等同于
function add(x, y) {return x + y;}
var foo = new Function( 'return "hello world"');
```

- function命令：函数的声明

  function命令后面是函数名，函数名后面是一对圆括号，里面是传入的参数，函数体放在大括号里面。这叫做函数的声明（Function Declaration）。

- 函数表达式：变量赋值

  将一个匿名函数赋值给变量，这个匿名函数又称函数表达式(Function Expression)，赋值语句的等号右边只能放表达式。

  使用函数表达式时，function命令后面不带函数名，如果加上函数名，该函数名只在函数体内部有效，在函数体外部无效。加上函数名的用处：1. 可以再函数体内部调用自身。 2. 方便除错(除错工具会显示这个名字，而不是匿名函数)

  函数表达式需要在语句的结尾加上分号表示语句结束。函数的声明在结尾的大括号后面不用加分号。

- Function构造函数

  Function构造函数可以传递任意数量的参数，只有最后一个参数会被当做函数体，如果只有一个参数，该参数就是函数体。Function构造函数可以不使用new命令，返回结果完全一样。这种方式非常不直观，几乎无人使用。

### 1.2 函数的重复声明：后面覆盖前面

由于函数名的提升，前一次声明在任何时候都是无效的。

```javascript
function f() {console.log('hello')}
f();	// world
function f() {console.log('world')}
f();	// world
```

### 1.3 函数调用、return语句、调用自身、函数是一种值

- 调用函数

  调用函数时，要使用圆括号运算符，如果有参数，参数写在圆括号中。

- return语句

  如果函数体内有return语句，则结束函数执行，直接返回return后面表达式的值。也就是说，函数的返回值可以使用return指定，如果没有return，函数就不返回任何值，或者说返回`undefined`。

- 调用自身：递归

  函数可以在函数体中使用函数名调用自身，也就是递归(recursion)。

  ```javascript
  // 通过递归，计算斐波那契数列
  function fib(num) {
    if (num === 0) return 0;
    if (num === 1) return 1;
    return fib(num - 2) + fib(num - 1);
  }
  fib(10)	// 55
  ```

- 函数是一种值

  JavaScript将函数看做一种值，与其他值(数值、字符串、布尔值等)低位相同。凡是可以使用值的地方，就能使用函数。如：可以把函数赋值给变量和对象的属性，也可以当作参数传入其他函数，或者作为函数的结果返回。函数只是一个可以执行的值，此外并无特殊之处。

  ```javascript
  function add(x, y) { return x + y; }
  // 将函数赋值给一个变量
  var operator = add;
  // 将函数作为参数和返回值
  function a(op){ return op; }
  a(add)(1, 1)	// 2
  ```

### 1.4 函数名提升

JavaScript引擎将函数名视同变量名，所以采用function命令声明的函数，整个函数会像变量声明一样，被提升到代码头部，所以后面定义的函数，前面就可以执行。

但是如果采用赋值语句定义函数，则函数不能提前调用，因为变量只是声明提前了，但是还没有赋值(undefined)，所以会报错，只能赋值后才能调用。

```javascript
f();	// 可以正常执行
function f() {console.log('f')}
g();	// TypeError: undefined is not a function
var g = fuhction (){};

h() // 2 函数声明提前了，所以 此时调用的是函数声明
var h = function () { console.log('1'); }
h() // 1	赋值的函数
function h() { console.log('2'); }
h() // 1 函数已经声明提前了，所以此处还是赋值的函数
```



- 不能在条件语句中声明函数

  由于存在函数名的提升，所以在条件语句中声明的函数在外面执行可能不会报错(chrome 浏览器会报错)。

  要达到在条件语句中定义函数的目的，只有使用函数表达式。 

  ```javascript
  if (false) { function x() {} }
  f() // 不报错	经测试chrome浏览器开发者工具报错
  // chrome:Uncaught ReferenceError: f is not defined
  
  if (false) { var f = function () {}; }
  f() // undefined chrome:TypeError: f is not a function
  ```



## 2. 函数的属性和方法

### 2.1 name属性

- name属性返回函数的名字
- 如果是通过变量赋值定义的函数，那么name属性返回变量名
- 如果变量赋值的是一个具名函数，那么返回function关键字之后的那个函数名
- name属性的一个用处：获取参数函数的名字

```javascript
function f1() {}
f1.name // "f1"
var f2 = function () {};
f2.name // "f2"
var f3 = function myName() {};
f3.name // 'myName'

var myFunc = function () {};
function test(f) { console.log(f.name); }
test(myFunc) // myFunc
```













## 参考资料

[函数 阮一峰](http://javascript.ruanyifeng.com/grammar/function.html)