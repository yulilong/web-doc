[TOC]



## 1. 对象是什么

面向对象编程(Object Oriented Programming,OOP)是目前主流编程范式。

它将真实世界各种复杂的关系抽象为一个个对象，然后由对象之间分工与合作，完成对真实世界的模拟。

面向对象编程具有灵活、代码可复用、高度模块化等特点，容易维护和开发，比起由一系列函数或指令组成的传统的过程式编程（procedural programming），更适合多人合作的大型软件项目。

- 对象是单个实物的抽象
- 对象是一个容器，封装了属性(property)和方法(method)

典型的面向对象语言(C++、Java)都有类(class)的概念：类就是对象的模板，对象是类的实例。

而JavaScript语言的对象体系是基于构造函数(constructor)和原型链(prototype).

构造函数相当于其他语言的类

原型链类相当其他语言的继承

## 2. 构造函数:JS的类

JavaScript语言中构造函数(constructor)：

> - 是对象的模板，描述实例对象的基本结构。实例对象的属性和方法，可以定义在构造函数内部
> - 是用来生成实例对象的函数
> - 是一个普通函数，但有自己的特征和用法
> - 为了与普通函数区别，构造函数名字第一个字母通常大写

构造函数的特点：

> - 函数体内部使用了this关键字，代表了所要生成的对象实例。
> - 生成对象的时候必须使用new命令。
> - 如果不用new命令就执行则会成为普通函数，此时会给this指向的对象创建变量，可使用严格模式防止忘记new命令,或在内部判断是否使用了new命令

```javascript
function Foo(foo, bar){
  // 'use strict';	// 在严格模式下，如果不指定this，则this是undefined
  // 或者使用判断是否使用了 new命令
  // if (!(this instanceof Foo)) {return new Foo(foo) }
  this.tt = 200;
}
// 使用上面注释部分代码可解决不使用new问题
Foo()			// 这里报错 TypeError: Cannot set property 'tt' of undefined
new Foo()).tt	// 正常访问
```





### 2.1 使用new命令生成一个对象

对构造函数使用new命令后：

> 1. 创建一个空对象(obj)，作为将要返回的对象的实例
> 2. 将obj的原型指向构造函数的prototype属性
> 3. 将obj赋值给函数内部的this关键字
> 4. 开始执行构造函数的内部代码

也就是说构造函数就是操作一个空对象将其“构造”为需要的样子。

使用new命令注意：

- new命令总是返回一个对象要么是实例对象，要么是return语句指定的对象，如果return的不是对象，则忽略return
- 如果普通函数(内部没有this)，new命令则会返回空对象
- new命令本身就可以执行构造函数，所以构造函数可以带括号，也可以不带。

```javascript
function A() { this.one = 200; return 30;}
console.log((new A()) === 1000)		// false
function B() { this.one = 200; return {tt: 10};}
console.log((new B()).tt)			// 10	构造函数使用括号
console.log((new B.tt)				// 10	构造函数没有使用括号
function hello(){return 'hello';}
console.log((new hello()))
```

#### 2.1.1 new.target

函数内部有一个属性：new.target，如果使用new命令调用函数则new.target指向当前函数，否则为undefined。

可使用该属性来判断调用函数的手是否使用了了new命令

```javascript
function f() { console.log(new.target === f); }
f() 	// false
new f() // true
```

### 2.2 Object.create() 创建实例对象

`Object.create`:是ES5方法,以现有的对象为模板生成新的实例对象。

创建一个对象：如果没有构造函数，只有对象，这个时候 Object.create就用到了，或者自己写一个克隆函数的方法。

```javascript
var person1 = { name: 'jack', };
var person2 = Object.create(person1);
console.log(person2.name)
```



## 3. prototype原型对象：继承

继承是面向对象重要特性，B对象继承A对象后，就能拥有A对象的所有属性和方法，对于代码复用非常有用。

大部分面向对象语言都是通过类(class)来实现继承， JavaScript的继承则是通过原型对象(prototype)实现的。

使用构造函数创建对象，虽然方便，但有个缺点：多个对象间无法共享属性(同样行为的方法、属性)，从而造成系统资源的浪费。

原型对象(prototype)可以解决这个问题。

### 3.1 函数的prototype属性

**JavaScript继承机制：**原型对象的所有属性和方法都能被实例对象共享。这么做不仅节省了内存，还体现了实例对象之间的联系。

**JavaScript规定：**每个函数都有一个prototype属性，指向一个对象。

对于普通函数该属性基本无用，但对于构造函数来说，生成实例的时候，该属性会自动成为实例对象的原型。

**原型对象的作用：**定义所有实例对象共享的属性和方法。而实例对象可以看做从原型对象衍生出来的子对象。

```javascript
function f() {}
console.log(typeof f.prototype) // "object"
function Animal(name) { this.name = name; }
Animal.prototype.color = 'white';
var cat1 = new Animal('kit');
var cat2 = new Animal('hello');
cat1.color	// white
cat2.color	// white
Animal.prototype.color = 'red';
cat1.color	// red
cat2.color	// red

cat1.color = 'yellow'
cat1.color	// yellow
cat2.color	// red
Animal.prototype.color = 'red';
// 如果修改了原型，那么此后新建的对象跟前面对象的原型则不是一个了
Animal.prototype = {hobby: 'eat'}
var cat3 = new Animal('jack')
```

原型对象的属性为所有实例对象共享。只要修改原型对象，变动就立刻会体现在**所有**实例对象上。

这是因为实例对象本身没有设个属性，都是读取原型对象的属性，也就是说当实例对象本身没有这个属性或方法的时候，它就会到原型对象去寻找该属性或方法，这就原型对象的特殊地方。

如果实例对象自身有这个属性，那么它就不会再去原型对象中寻找这个属性。

使用构造函数创建对象后，此时修改构造函数的原型，那么在此新建的对象原型就跟之前的原型不一样了。

### 3.2 原型链

**JavaScript规定：**所有对象都有自己的原型对象。

**原型链：** 任何一个对象都可以充当其他对象的原型，由于原型对象也是对象，所以它也有自己的原型，因此就会形成一个原型链：对象到原型 -> 原型的原型 。。。。。。。。

实例对象的原型一层层上溯，最终都可以上溯到`Object.prototype`,即Object构造函数的prototype属性。这就是所有对象都有`valueOf`和`toString`方法的原因。

`Object.prototype`对象的原型是`null`,`null`没有任何属性和方法，也就没有自己的原型，因此，**原型链的尽头是`null`**。

**JS引擎寻找对象的属性**：

1. 从对象本身上找
2. 对象本身上找不到，就到他的原型上去找
3. 如果原型上找不到，就到原型的原型上去找，
4. 如果直到顶层的`Object.prototype`还没有找到，则返回`undefined`
5. 如果对象自身和它的原型都定义了同名属性，则优先读取对象自身的属性，叫**覆盖(overriding)**

在整个原型链上寻找属性，对性能是有影响的。



### 3.3 constructor属性

prototype对象上有一个constructor属性，默认指向prototype对象所在的构造函数。可以被所有实例对象继承。

constructor属性：

> 可以知道实例对象是哪一个构造函数创建的。
>
> 可以通过实例对象的constructor属性新建另一个实例对象。
>
> constructor表达了原型对象和构造函数的关联关系，如果修改了原型对象，要同时修改constructor属性，防止引用时出错。
>
> `constructor.name`属性可以知道构造函数的名称



```javascript
function F() {};
var f = new F();
f.constructor === F 		// true
f.constructor === Object 	// false
var y = new f.constructor();
y instanceof F				// true
// 调用构造函数，新建一个实例
F.prototype.createF = function () {
  return new this.constructor();
};
// 修改了原型，同时也要修改constructor
F.prototype = {  method: function () {} };
F.prototype.constructor = F;
console.log((new F()).constructor.name)	// "F"
```

要么将`constructor`属性重新指向原来的构造函数，要么只在原型对象上添加方法，这样可以保证`instanceof`运算符不会失真。



## 4. instanceof运算符:判断对象的类型

instanceof运算符返回一个布尔值，表示对象是否为某个构造函数的实例。

instanceof运算符的左边是实例对象，右边是构造函数，它会检查构造函数的原型对象是否在对象的原型链上，因此同一个实例对象，可能会对多个构造函数都返回`true`。

有一种特殊情况，就是左边对象的原型链上，只有`null`对象。这时，`instanceof`判断会失真。

但是，只要一个对象的原型不是`null`，`instanceof`运算符的判断就不会失真。

**注：**

>  instanceof只能用于对象，不适用原始类型的值，原始值返回false。
>
> 对于`undefined`和`null`，`instanceOf`运算符总是返回`false`。
>
> 利用instanceof运算符解决调用构造函数时，忘记加new命令的问题。

```javascript
var d = new Date();
d instanceof Date // true
d instanceof Object // true
Object.create(null) instanceof Object // false

'hello' instanceof String	// false
undefined instanceof Object // false
function F (foo) {
    if (!(this instanceof F) { } // 没有使用new操作符
}
```









## 参考资料



[构造函数与 new 命令 阮一峰](http://javascript.ruanyifeng.com/oop/basic.html)

[prototype原型 阮一峰](http://javascript.ruanyifeng.com/oop/prototype.html)

