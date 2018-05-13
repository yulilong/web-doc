[TOC]

## 1. 概述

JavaScript是一种动态类型语言，变量没有类型限制，可以随时赋予任何值。

变量的类型无法再编译阶段确定，必须要在运行时才能知道。

虽然变量类型不确定，但各种运算符对数据类型是有要求的，如果运算符发现变量的类型与预期不符，就会自动转换类型。如减法运算符期望左右两侧的变量是数值，如果不是就会自动将他们转换为数值：

```javascript
'250' - '50'	// 200
```



## 2. 强制类型转换

主要使用`Number(obj)`、`String(obj)`、`Boolean(obj)`三个函数，手动将其他类型的变量转换为数字、字符串、布尔值。

### 2.1 强制转为数字：Number()、parseInt()、parseFloat(string)

#### 2.1.1 Number(value)

介绍：将其他类型的值转化成数字。Number函数整体转换，有一个无法转换就会返回NaN，parseInt和parseFloat则是逐个解析字符。

参数：value：待转换的值

 转换规则：

| 参数类型  | 转为数值的规则                                               | 举例                                           |
| --------- | ------------------------------------------------------------ | ---------------------------------------------- |
| Number    | 不变                                                         | `Number(123) // 123`                           |
| String    | 如果可以被解析，转为相应数值，否则为NaN，空串和空白符( 空格、制表符、换页符和换行符)转为0 | '123' => 123, '12ab' => NaN, '' =>0, '\n' => 0 |
| Boolean   | true：1，false：0                                            | true => 1, false => 0                          |
| undefined | 转为 NaN                                                     | undefined => NaN                               |
| null      | 转为0                                                        | null => 0                                      |
| Object    | 转为NaN，但：包含单个数值的数组会返回对应数值                | {} => NaN, [1] => 1,                           |

- Number对于对象的转换规则：

  > 1. 调用对象自身的`valueOf`方法，如果是原始类型的值，则直接使用Number函数，结束
  > 2. 如果`valueOf`方法返回的还是对象，则调用对象的`toString`方法，如果返回原始类型，则直接使用Number函数，结束
  > 3. 如果`toSrting`方法返回的是对象，就报异常(Uncaught TypeError: 对象不能转为原始类型)，结束

  ```javascript
  var obj = {
    valueOf: function () { return {}; },
    toString: function () { return {}; }
  };
  Number(obj)
  ```

  ​

#### 2.1.2 parseInt(string, radix)

介绍：解析一个字符串参数，并返回一个指定数字进制格式(二、十、十六进制)。

参数：String：字符串，如果不是字符串会被转为字符串,radix：个2到36之间的整数值，用于指定转换中采用的基数，如2，10，16。如果忽该参数，可能会产生不同结果。

转换结果：

> - 如果输入的参数无法转化为数值类型，则返回NaN， 空字符串也返回Nan。
> - 字符串的开头的空白字符会被忽略，直到找到第一个非空白字符开始转换。
> - 从第一个字符开始，直到遇到非数字字符或结尾结束，返回解析的整数部分，非数字部分忽略。
> - 如果设置了第二个参数，则可以把数字转换到相应进制(二进制、十进制、十六进制)

```javascript
parseInt(" \n132.44ddd");	// 132
parseInt("0xF", 16);		// 15
parseInt("546", 2);   		// Nan , 除了“0、1”外，其它数字都不是有效二进制数字
arseInt(" \nddd");			// NaN
```



#### 2.1.3 parseFloat(string)

介绍：把一个字符串解析为浮点数并返回，parseFloat是个全局函数,不属于任何对象.

参数： String：需要解析的字符串

转换结果：

> - 如果参数不能解析成数字，则返回NaN，parseFloat只能返回十进制数
> - 如果遇到了与浮点数无关的字符，则函数停止解析，返回已经解析到的浮点数，
> - 字符串的头部空白字符会被忽略
> - 如果字符串没有小数点或小数点后都是零，则返回整数，字符串中第一个小数点是有效的。第二则无效。
> - 与浮点数相关的字符：正负号(+或-),数字(0-9),小数点,或者科学记数法中的指数(e或E)

```javascript
parseFloat("0.0314E+2");		// 3.14
parseFloat('  \n .12345');		// 0.12345
parseFloat('  \n .12.345');		// 0.12
rseFloat('dsss')				// NaN
```



### 2.2 强制转换为字符串：String(value)

介绍：String函数可以将任意类型的值转化成字符串，

参数： 待转换的值。

转换规则：

| 参数类型  | 返回结果                                              | 举例                             |
| --------- | ----------------------------------------------------- | -------------------------------- |
| Number    | 转为相应的字符串                                      | String(123) // "123"             |
| String    | 不变                                                  | String('abc') // "abc"           |
| Boolean   | true： "true", false: "false"                         | String(true) // "true"           |
| undefined | "undefined"                                           | String(undefined) // "undefined" |
| null      | "null"                                                | String(null) // "null"           |
| Object    | `{a: 1}`: "[object Object]",  数组:  数组的字符串形式 | String([1, 2, 3]) // "1, 2, 3"   |
| NaN       | "NaN"                                                 | String(NaN)  // "NaN"            |

- String对于对象的转换规则：

  > 1. 先调用对象的toString方法，如果返回原始类型的值，则调用String函数，结束
  > 2. 如果toString方法返回的是对象，再调用对象的valueOf方法，如果返回原始类型的值，则调用String函数，结束。
  > 3. 如果valueOf方法返回的是对象，就报异常(Uncaught TypeError: 对象不能转为原始类型)，结束

  ```javascript
  var obj = {
    valueOf: function () { return {}; },
    toString: function () { return {}; }
  };
  String(obj)
  ```

#### 2.2.1 其他转为字符串的方法

1. "" + value
2. value.toString()

### 2.3 强转为布尔：Boolean()

`Boolean`函数可以将任意类型的值转为布尔值。

转换规则：

| 值                                        | 转换结果 |
| ----------------------------------------- | -------- |
| undefined                                 | false    |
| null                                      | false    |
| 0(-0,+0)                                  | false    |
| NaN                                       | false    |
| ''(空字符串)                              | false    |
| 所有对象(包括空对象)(new  Boolean(false)) | true     |
| 其他                                      | true     |

所有对象的布尔值都是true，是JavaScript出于性能的考虑，统一规定，如：`obj1 && obj2`

```javascript
// 浏览器打开开发者工具， Console里面测试
Boolean(undefined)			// false
Boolean(null)				// false
Boolean(0)					// false
Boolean(NaN)				// false
Boolean('')					// false
Boolean({})					// true
Boolean([])					// true
Boolean(new Boolean(false))	// true
```



## 3. 自动类型转换

自动转换是以强制转换为基础的，JavaScript会自动转换数据类型。

### 3.1 出现自动类型转换的情况

- `==`非严格判断相等
- 不同的数据类型互相运算
- 条件判断中：数据求布尔值
- 对非数值的变量使用一元运算符(+,-)

```javascript
123 + 'abc'		// "123abc"
if ('abc') {}
+ {foo: 'bar'}
- [1, 2, 3]
'123' == 1
```

### 3.2 `==`非严格判断相等的转换规则

在使用`==`判断相等的时候，如果两个值类型相等，那么执行严格相等判断，如果类型不同，则会自动做类型转换为相同然后在执行严格相等判断。

对于`a == b`的比较规则：

|      |
| ---- |
|      |