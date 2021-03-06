---
layout: post
title: Javascript（一）
categories:
- ES5
subhead: javascript - 基础
---

# Javascript

## 基础
javascript术语基本涵盖了以下三个部分：

* `ECMAScript` - 语言的核心部分（即变量，函数，和循环等等）。
* `DOM`（文档对象模型）- DOM标准（与HTML，XML文档交互的方式）。
* `BOM`（游览器对象模型）- 与游览器有关的对象集合。

面向对象程序设计的OOP常用到的概念：

* 对象（有时候也可以称作为"实例"）、方法、属性；
* 类 - 原型系统prototype，没有类的概念可以理解为模板；
* 封装 - 我们只需要知道所操作对象的接口，而不必去关心它的具体实现；
* 聚合 - 多个对象合并成一个新对象的过程；
* 重用和继承 - 实现代码的重用；
* 多态 - 不同的对象通过相同的方法调用来实现各自行为；
<!--break-->
### 操作符

* `+` - 加法运算

* `-` - 减法运算

* `*` - 乘法运算

* `/` - 除法运算

* `%` - 求余运算

* `++` - 自增1运算

```js
var a = 0;
var b = a++;
// b = 0;

var a = 0;
var b = ++a;
// b = 1;
```

* `--` - 自减1运算

```js
var a = 1;
var b = a--;
// b = 1;

var a = 1;
var b = --a
// b = 0;
```

* 复合操作符 `+=`，`-=`等。

### 数据类型
基本类型（原始类型）：

1. 数字 - 包括浮点数和整数：1、100、3.14。

2. 字符串 - 包括由任意数量字符组成的序列："a"，"one"，"one 2 three"。

3. 布尔值 - true 和 false

4. undefined

5. null

非基本类型（对象类型）：

1. 对象 - 特殊的对象包括（数组、函数）。如果函数使用 `new` 运算符新建一个对象，变将其称之为构造函数。类可以看做是对象类型的子类型，一共
有五种：数组类，函数类，日期类，正则类，错误类。

#### 数字
数字运算的 `Math` 对象。

* 无穷大 `Infinity`
* 负无穷大 `-Infinity`
* 非数字 `NaN` - 它和任何值都不相等，包括自身。

函数 `isFinite()` 在不是 `NaN`, `Infinity`, `-Infinity` 的时候返回 `true`。

用函数 `isNaN()` 在是 `NaN` 或者一个非数字值（字符串或者对象）的时候返回 `true`。
```js
Math.pow(2,53)          // 9007199254740992 2的53次幂
Math.round(.6)          // 1 四舍五入
Math.ceil(.6)              // 1 向上取整
Math.floor(.6)            // 0 向下取整
Math.abs(-5)             // 5 求绝对值
Math.max(2,3,5)        // 5 返回最大值
Math.min(2,3,5)         // 2 返回最小值
Math.random()          // 生成一个 >= 0 & < 1 的伪随机数
Math.PI                      // π 圆周率
Math.E                       // e 自然对数的底数
Math.sqrt(4)             // 2 4的平方根
Math.pow(8,1/3)        // 2 8的立方根
Math.sin(0)               // 三角函数。还有：Math.cos,Math.atan等
Math.log(10)              // 10的自然对数
Math.log(100)/Math.LN10 // 以10为底的100的对数
Math.exp(3)               // e的三次幂
```

#### 字符串
字符串是固定不变的。类似 `replace()` 和 `toUpperCase()` 都是返回新的字符串，原本的字符串并未发生改变。

字符串可以当做只读数组。
```js
var s = 'hello, world!'

// h 第一个字符
s.charAt(0)
// 类似于
s[0]

// d 最后一个字符
s.charAt(s.length - 1)

// ll 第三个到第四个字符
s.substring(2,4)

// ll 同上
s.slice(2,4)

// rld 最后三个字符
s.slice(-3)

// 2 首次出现"l"的位置
s.indexOf("l")

// 10 最后次出现"l"的位置
s.lastIndexOf("l")

// 3 在3位置及之后首次出现"l"的位置
s.indexOf("l",3)

// ["hello", " world"] 分割成子串
s.split(',')

// Hello, world 全文字符替换
s.replace("h", "H")

// HELLO, WORLD
s.toUpperCase()
```

#### 布尔值
下面的值都会转为 `false`
```
undefined
null
0
-0
NaN
""
```

#### null和undefined
```
null == undefined // true

null === undefined // false

typeof(null) // object

typeof(undefined) // undefined
```

#### 对象（引用类型）
对象的比较并非值的比较，即便两个对象包含相同的属性及相同的值，它们也是不相等的。各个索引元素完全相同的数组也不相等。
```js
var a = {x:1}, b = {x:1}
a === b // false

var c = [], d = []
c === d // false
```
对象值都是引用，对象的比较都是引用的比较，当且仅当它们引用同一个基对象时，它们才相等。
```js
var a = [];
var b = a;
b[0] = 1;
a === b // true;
```
- 内置对象：
    * 数组
    * 函数
    * 日期
    * 正则表达式
- 宿主对象
- 自定义对象
- 自由属性
- 继承属性

对象的创建：
* 对象直接量
* new
* Object.create()

对象的枚举：
* for/in
* Object.keys()
* Object.getOwnPropertyNames()


### 变量
变量的使用步骤：
1. 变量的声明
2. 变量的赋值

```js
var a = 1;
```

变量名可以由字母、数字、下划线及美元符号组合而成，但不能以数字开头。

变量名区分大小写。

#### 变量的作用域
在函数体内，局部变量的优先级高于全局的同名变量。
```js
var scope = "global";

function check () {
    var scope = "local";
    console.log(scope);
}

check();      // local;
```
当使用 `var` 声明一个变量时，无法使用 `delete` 删除。
```js
var a = 1;
delete a;
a // 1;
```
但是如果是在非严格模式下，并且给一个非声明的变量赋值，`JavaScript` 会自动创建一个对象。那么这个变量是可以被删除的。
```js
a = 1;
delete a;
a // a is not defined
```

### 函数
函数作用域和声明提前。

函数声明语句的函数名称和函数体均提前。

其语法如下：
```
function funcname([args1 [,args2[...,argsn]]]) {
    statements
}
```

### 语句
* 条件语句 - `if`，`if/else`，`else if`，`switch`
* 循环语句 - `while`，`do/while`，`for`，`for/in`
* 跳转语句 - `break`，`return`，`throw`，`continue`
* 其他类型语句 - `with`，`debugger`，`use strict`

#### 异常 throw
```
throw new Error('这个一个错误！')
```

```
try {

}
catch (e) {

}
finally {

}
```

