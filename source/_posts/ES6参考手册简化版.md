---
title: ES6参考手册简化版
top: false
cover: false
toc: true
mathjax: true
date: 2021-08-18 19:43:49
password:
summary:
tags: [web,ES6]
categories: ES6
---

# ES6简介

> **ECMAScript 6.0（以下简称 ES6）是 JavaScript 语言的下一代标准，已经在 2015 年 6 月正式发布了，也叫ECMAScript 2015**



# 块级作用域

## ES5作用域缺陷

~~~js
function fn() {
  var a = 'hello';
}
fn();
console.log(a); // Uncaught ReferenceError: a is not defined

// 解析：变量a只在函数作用域中有效，a在块级作用域{}里面
~~~

ES6之前 只有`全局作用域`和`函数作用域`，没有块级作用域，带来很多不合理的场景

**第一种场景**

内层变量可能会覆盖外层变量

```js
var a = 'aaa';

function fn() {
  console.log(a); // 预解析：就是在浏览器解析代码之前，把变量的声明和函数的声明提升到该作用域的最上面
  if (false) {
    var a = 'bbb';
  }
}

fn(); // undefined
```

相当于

~~~js
var a = 'aaa';
function fn() {
  var a;
  console.log(a); // 变量声明了但没有赋值，结果是undefined
  if (false) {
    var a = 'bbb';
  }
}
~~~



**第二种场景**

用来计数的循环变量泄露为全局变量

```js
for (var i = 0; i < 5; i++) {
  // code
}
console.log(i); // 5 由于i没有采用块级作用域，那么i的作用域是全局的，打印结果是5
```

**解决办法**

~~~js
for (let i = 0; i < 5; i++) {
  // code
}
console.log(i); // Uncaught ReferenceError: i is not defined
~~~



## ES6块级作用域

* 花括号 {} 和其中代码生成一个块
* 在块中，**let**和**const**声明的变量和常量对外都是不可见的，称之为块级作用域
* 只有使用**let**和**const**声明的变量或者常量在块中对外不可见，**var**声明的变量对外依然可见



```js
function fn() {
  let a = 5;
  if (true) {
    let a = 10;
  }
  console.log(a);
}
fn(); // 5
```

上面的函数有两个代码块，都声明了变量n，运行后输出 5，这表示外层代码块不受内层代码块的影响。如果两次都使用var定义变量n，最后输出的值才是 10

```js
function fn() {
  var a = 5;
  if (true) {
    var a = 10;
  }
  console.log(a);
}
fn() // 10
```





# let 和 const

## let

~~~js
// 用来声明变量
{
  let num = 1;
  let str = 'hello world';
}


// 不可以重复声明
{
  let a = 1;
  let a = 2; // Uncaught SyntaxError: Identifier 'a' has already been declared
}


// 不存在变量提升
{
  console.log(a); // ReferenceError: a is not defined
  let a = 2;
}


// 只在声明所在的块级作用域内有效
{
  let a = 1;
  console.log(a); // 1
  var b = 2;
}
console.log(a); // Uncaught ReferenceError: a is not defined
console.log(b); // 2
~~~

示例

~~~js
var a = 10;
function fn() {
  console.log(a);
  let a = 20;
}
fn(); // Uncaught ReferenceError: Cannot access 'a' before initialization

// 解析：初始化前无法访问a
~~~



## const

~~~js
// 用来声明常量（不可改，只读）
{
  const PI = 3.14;
}


// 不可以重新赋值
{
  const a = 1;
  a = 2; // Uncaught TypeError: Assignment to constant variable.
}


// 声明的时候必须初始化（赋值）
{
  const a;
  a = 10; // Uncaught SyntaxError: Missing initializer in const declaration
}


// 不可以重复声明
{
  const a = 10;
  const a = 20; // Uncaught SyntaxError: Identifier 'a' has already been declared
}


// 不存在变量提升
{
  console.log(a); // Uncaught ReferenceError: a is not defined
  const a = 5;
}


// 只在声明的块级作用域内有效
{
  const a = 10;
  console.log(a); // 10
}
console.log(a); // Uncaught ReferenceError: a is not defined
~~~

复合类型的数据（主要是对象和数组），可以这样子变动（它们在栈中的引用地址没变）

~~~js
{
    const obj = {};
    obj.name = 'abc';
    
    // 将 foo 指向另一个对象，就会报错
    obj = {}; // Uncaught TypeError: Assignment to constant variable
}
~~~

~~~js
{
    const arr = [];
    arr.push(123);
}
~~~



## 区别

~~~js
// 相同点：
	1. 都不存在变量提升
	2. 都只在声明的块级作用域内有效

// 不同点：
	1. 声明类型： let 声明变量， const 声明常量
  2. 赋值时机： let 可以声明变量与给变量赋值分开，使用 const 声明常量的时候必须同时赋值，否则报错
~~~

**推荐**

~~~js
// 对于 数值、字符串、布尔值 经常会变的，用 let 声明
{
    let num = 10;
    let str = 'abc';
    let flag = true;
}

// 对象、数组和函数用 const 来声明
{
    const obj = {};
    const arr = [];
    const fn = function() {}
}
~~~





# 解构赋值

## 数组解构赋值

**一次性声明多个变量**

~~~js
{
	let [a, b, c, d] = [1, 2, 3];
	console.log(a); // 1
	console.log(b); // 2
	console.log(c); // 3
	console.log(d); // undefined
}
~~~



**结合扩展运算符**

~~~js
{
	let [a, b, ...c] = [1, 2, 3, 4, 5];
	console.log(a); // 1
	console.log(b); // 2
	console.log(c); // [3, 4, 5]
}
~~~



**允许指定默认值**

~~~js
{
	let [a, b, c = 3] = [1, 2];
  
	console.log(a); // 1
	console.log(b); // 2
	console.log(c); // 3
}
~~~



~~~js
{
	let [a, , , b] = [1, 2, 3, 4, 5];
	console.log(a, b); // 1, 4
}
~~~



~~~js
{
	let [a, , ...b] = [1, 2, 3, 4, 5];
	console.log(a, b); // 1, [3, 4, 5]
}
~~~



应用场景

~~~js
// 变量交换
{
	let a = 1;
	let b = 2;
	[a, b] = [b, a];
	console.log(a, b); // 2, 1
}
~~~



## 对象解构赋值

数组中，变量的取值由它 **排列的位置** 决定；而对象中，变量必须与 **属性** 同名，才能取到正确的值

**变量与属性同名**

~~~js
{
	let { a, b } = { a: 1, b: 2 };
	console.log(a); // 1
	console.log(b); // 2
}
~~~

~~~js
{
  let obj = { b: 2, a: 1 };
	let { a, b, c } = obj;
	console.log(a); // 1
	console.log(b); // 2
  console.log(c); // undefined
}
~~~



**允许指定默认值**

~~~js
{
	let { a, b = 2 } = { a: 1 };
	console.log(a); // 1
	console.log(b); // 2
}
~~~



**允许重命名**

~~~js
{
  let { a: res } = { a: 1, b: 2 };
  console.log(a); // ReferenceError: a is not defined （原名a变无效）
  console.log(res); // 1
}
~~~



## 函数参数解构赋值

**函数参数的默认值**

~~~js
function fn(a = 1, b = 2){
	return a + b;
}
fn() // 3  默认 a = 1, b = 2
fn(3) // 5  因为 a = 3, b = 2
fn(3，3) // 6  因为 a = 3, b = 3
~~~



**函数参数的默认值（对象参数）**

~~~js
function fn({a = 1, b = 2} = {}) {
  console.log(a, b);
}
fn(); // 1 2
fn({ a: 2}); // 2 2
fn({ a: 3, b: 6}); // 3 6
~~~



## 字符串解构

字符串也可以解构赋值，这是因为此时，字符串被转换成了一个类似数组的对象

**字符串解构**

~~~js
{
  const [a, b, c, d, e] = 'hello';
	console.log(a); // h
	console.log(b); // e
	console.log(c); // l
	console.log(d); // l
	console.log(e); // o
}
~~~



**把字符串转为数组**

~~~js
{
  const [...a] = 'hello';
	console.log(a); // ["h", "e", "l", "l", "o"]
}
~~~





# 字符串扩展

## 模板字符串

**`模板字符串`** 用反引号（``）标识。它可以当作普通字符串使用，也可以用来定义多行字符串，或者在字符串中嵌入变量。

**字符串中嵌套变量**

原生JS写法

~~~js
var a = 1;
var b = 2;
console.log('a + b = ' + (a + b)); // a + b = 3
~~~

~~~js
var name = 'A';
var age = 18;
console.log('my name is '+ name + 'and my age is ' + age); // my name is A my age is 18
~~~

ES6 写法

~~~js
// 字符串中嵌入变量	模板字符串中嵌入变量，需要将变量名写在 ${ } 之中,可放入表达式
var a = 1;
var b = 2;
console.log(`a + b = ${a + b}`); // a + b = 3
~~~

~~~js
var name = 'A';
var age = 18;
console.log(`my name is ${name} and my age is ${age}`); // my name is A my age is 18
~~~

~~~js
var obj = { 
    a: 1,
    b: 2
}
console.log(`${obj.a + obj.b}`); // 3
~~~

~~~js
var fn = (name) => `Hello ${name}!`;
fn('abc'); // "Hello abc!"
~~~

**可调用函数**

~~~js
// 可以调用函数
function fn() {
  return 'abc';
}

`one ${fn()} one`
// one abc one
~~~

注意：如果在模板字符串中需要使用反引号，则前面要用反斜杠转义

~~~js
let a = `\`Hello\` World!`; // `Hello` World!
~~~



## 字符串函数

| 函数         | 含义                                           |
| ------------ | ---------------------------------------------- |
| includes()   | 返回布尔值，表示是否找到了参数字符串           |
| startsWith() | 返回布尔值，表示参数字符串是否在原字符串的头部 |
| endsWith()   | 返回布尔值，表示参数字符串是否在原字符串的尾部 |

~~~js
{
	let str = 'Hello world!';
	str.startsWith('Hello'); // true
	str.endsWith('!'); // true
	str.includes('o'); // true
}
~~~

这三个方法都支持第二个参数，表示开始搜索的位置

~~~js
{
	let str = 'Hello world!';
	str.startsWith('world', 6); // true
	str.endsWith('Hello', 5); // true
	str.includes('Hello', 6); // false
}
~~~



| 函数       | 含义       |
| ---------- | ---------- |
| repeat()   | 字符串重复 |
| padStart() |            |
| padEnd()   |            |

~~~js
{
	let str = 'abc';
	console.log(str.repeat(2));// abcabc
}
~~~

字符串填补（多用于日期：2019-09-01）

~~~js
{
	let str = '1';
	console.log(str.padStart(2, '0')); // 01
	console.log(str.padStart(3, '0')); // 001
	console.log(str.padEnd(2, '0')); // 10
	console.log(str.padEnd(3, '0')); // 100
}
~~~





# 数组的扩展

**扩展运算符**（spread）是三个点（…），它好比 rest 参数的逆运算，将一个数组转为用逗号分隔的参数序列

## 扩展运算符

**展开数组**

~~~js
console.log(...[1, 2, 3]); // 1 2 3
console.log(1, ...[2, 3, 4], 5); // 1 2 3 4 5
~~~

注意，只有函数用时，扩展运算符才可以放在圆括号中

~~~js
(...[1, 2]); // 报错
~~~



**数组合并**

~~~js
const a = [1, 2, 3];
const b = [4, 5, 6];

// ES5 的数组合并
a.concat(b); // [1, 2, 3, 4, 5, 6]

// ES6 的数组合并
[...a, ...b] // [1, 2, 3, 4, 5, 6]
~~~



**函数调用**

~~~js
function add(a, b) {
  return a + b;
}

const arr = [2, 3];
add(...arr); // 5
~~~



**替代 apply **

由于扩展运算符可以展开数组，所以不再需要apply方法，将数组转为函数的参数了

~~~js
function fn(a, b, c) {
  console.log(a, b, c)
}
var arr = [1, 2, 3];

// ES5 的写法
fn.apply(null, arr); // 1 2 3

// ES6的写法
fn(...arr); // 1 2 3
~~~

~~~js
// ES5 的写法
Math.max.apply(null, [3, 9, 6]);

// ES6 的写法
Math.max(...[3, 9, 6]);

// 等同于
Math.max(3, 9, 6);
~~~

将一个数组添加到另一个数组的尾部

~~~js
// ES5的 写法
var arr1 = [0, 1, 2];
var arr2 = [3, 4, 5];
Array.prototype.push.apply(arr1, arr2);

// ES6 的写法
let arr1 = [0, 1, 2];
let arr2 = [3, 4, 5];
arr1.push(...arr2);
~~~



**与解构赋值结合**

~~~js
const [a, ...b] = [1, 2, 3];
a // 1
b // [2, 3]

const [a, ...b] = [];
a // undefined
b // []

const [a, ...b] = ["foo"];
a  // "foo"
b  // []
~~~

如果将扩展运算符用于数组赋值，只能放在参数的最后一位，否则会报错

~~~js
const [...a, b] = [1, 2, 3]; // 报错
const [a, ...b] = [1, 2, 3];
~~~



**复制数组**

~~~js
const a = [1, 2];
const b = a;

b[0] = 2;
a // [2, 2]
~~~

以下两种写法，不会修改原来的数组

~~~js
const a = [1, 2];

// 写法一
const b = [...a];

// 写法二
const [...b] = a;

b[0] = 2;
a // [1, 2]
~~~

不过，是浅拷贝，使用的时候需要注意



**将字符串转为真正的数组**

~~~js
[...'hello']
// [ "h", "e", "l", "l", "o" ]
~~~



## 数组函数

| 函数        | 含义                                                         |
| ----------- | ------------------------------------------------------------ |
| includes()  | 方法返回一个**布尔值**，判断数组是否包含给定的值，与字符串的 includes 方法类似 |
| find()      | 返回符合传入测试（函数）条件的数组元素                       |
| findIndex() | 返回符合传入测试（函数）条件的数组元素索引                   |
| for…of      | 数组遍历                                                     |
| Array.of()  | 方法用于将一组值，转换为数组                                 |

**includes()**

~~~js
[1, 2, 3].includes(2); // true
[1, 2, 3].includes(4); // false
[1, 2, NaN].includes(NaN); // true
~~~

该方法的第二个参数表示搜索的起始位置，默认为 0。如果第二个参数为负数，则表示倒数的位置，如果这时它大于数组长度（比如第二个参数为 -4，但数组长度为 3 ），则会重置为从 0 开始

~~~js
[1, 2, 3].includes(3, 3); // false
[1, 2, 3].includes(3, -1); // true
~~~



**find() 和 findIndex()**

```js
[1, 2, 3, 4, 5].find((item) => item > 3); // 4  -可以看到只返回一个值

[1, 2, 3, 4, 5].findIndex((item) => item > 3); // 3  -返回索引
```

~~~js
[1, 2, 3, 4, 5].find((item, index, arr) => item > 9); // -1  -所有成员都不符合条件，则返回-1
~~~

两个方法都可以发现`NaN`，弥补了数组的`indexOf`方法的不足

```javascript
[NaN].indexOf(NaN); // -1
[NaN].findIndex(y => Object.is(NaN, y)); // 0
```



**for ... of数组遍历**

直接得到数组的值

~~~js
var arr = [10, 20, 30];
for(var i of arr) {
	console.log(i);
}

// 10
// 20
// 30
~~~

~~~js
var arr = [{a: 10}, {b: 20}, {c: 30}];
for(var i of arr) {
	console.log(i);
}

// {a: 10}
// {b: 20}
// {c: 30}
~~~



`keys()` 是对**键名**的遍历		`values()`是对**值**的遍历		`entries()` 是对**键值对**的遍历

~~~js
for (let index of [1, 2].keys()) {
  console.log(index);
}
// 0
// 1

for (let val of [1, 2].values()) {
  console.log(val);
}
// 1
// 2

for (let [index, val] of [1, 2].entries()) {
  console.log(index, val);
}
// 0 1
// 1 2
~~~



**Array.of()**

~~~js
Array.of(1, 2, 3); // [1, 2, 3]

Array.of(3); // [3]

Array.of(); // []

Array.of(undefined); // [undefined]
~~~

与`Array()`的区别

```javascript
Array(); // []

Array(3); // [, , ,]

Array(1, 2, 3); // [1, 2, 3]

Array(undefined); // [undefined]
```





# 对象的扩展

## 属性简写

~~~js
const foo = 'bar';
const baz = {foo};
console.log(baz) // {foo: "bar"}

// 等同于
const baz = {foo: foo};
~~~

上面代码中，变量`foo`直接写在大括号里面。这时，属性名就是`变量名`, 属性值就是`变量值`

~~~js
let a = 1;
let b = 2;

const es5 = {
	a: a
	b: b
}
const es6 = {
  a,
  b
}
console.log(es6); // {a: 1, b: 2}
~~~

~~~js
function fn(a, b) {
  return {a, b};
}

// 等同于
function fn(a, b) {
  return {a: a, b: b};
}

fn(1, 2) // {a: 1, b: 2}
~~~



## 方法简写

~~~js
const es6 = {
	say() {
		return 'hello wrold';
  }
};

// 等同于
const es5 = {
  say: function() {
    return 'hello wrold';
  }
};
~~~



## 属性表达式

~~~js
{
  let a = 'b';
  let es5 = {
    a:'c'
    b:'c'
  };
  
  let es6 = {
   	[a]:'c' // 相当于上面 b:'c'
  }
}
~~~



## 扩展运算符

~~~js
let { a, b, ...c } = { a: 1, b: 2, c: 3, d: 4 };
a // 1
b // 2
c // { c: 3, d: 4 }
~~~

由于解构赋值要求等号右边是一个对象，所以如果等号右边是`undefined`或`null`，就会报错，因为它们无法转为对象

```javascript
let { ...a } = null; // 报错
let { ...a } = undefined; // 报错
```

解构赋值必须是最后一个参数，否则会报错

~~~js
let { ...a, b, c } = obj; // 报错
let { a, ...b, ...c } = obj; // 报错
~~~

注意，解构赋值的拷贝是浅拷贝，即如果一个键的值是复合类型的值（数组、对象、函数）、那么解构赋值拷贝的是这个值的引用，而不是这个值的副本

```javascript
let obj = { a: { b: 1 } };
let { ...newObj } = obj;
obj.a.b = 2;
console.log(newObj.a.b); // 2
```



## 对象API

判断两个字符串是否相等

~~~js
'abc' === 'abc'; // true
Object.is('abc', 'abc'); // true
~~~

判断两个数组是否相等

~~~js
[] === []; // false
Object.is([], []); // false

// 解析：两个数组引用的是两个不同的地址
~~~

拷贝对象

~~~js
Object.assign({a: 1}, {b: 2}); // {a: 1, b: 2}  浅拷贝
~~~

遍历对象

~~~js
{
	const obj = {a: 1, b: 2, c: 3};
  for(let [key, value] of Object.entries(obj)) {
  	console.log([key, value]);
  }
}
// ['a', 1]
// ['b', 2]
// ['c', 3]
~~~

**Object.assign()**

Object.assign方法用于对象的合并，将源对象（source）的所有可枚举属性，复制到目标对象（target）

~~~js
const target = { a: 1 };
const source1 = { b: 2 };
const source2 = { c: 3 };
Object.assign(target, source1, source2);
console.log(target); // {a: 1, b: 2, c: 3}
~~~

Object.assign方法的第一个参数是目标对象，后面的参数都是源对象。

**注意，如果目标对象与源对象有同名属性，或多个源对象有同名属性，则后面的属性会覆盖前面的属性。**

~~~js
const target = { a: 1, b: 1 };
const source1 = { b: 2, c: 2 };
const source2 = { c: 3 };
Object.assign(target, source1, source2);
console.log(target); // {a: 1, b: 2, c: 3}
~~~

Object.assign 方法实行的是浅拷贝，而不是深拷贝

~~~js
const obj1 = {a: {b: 1}};
const obj2 = Object.assign({}, obj1);
obj1.a.b = 2; // 修改b
obj2.a.b; // 2, 也改变了 
~~~

上面代码中，源对象 obj1 的 a 属性的值是一个对象，Object.assign 拷贝得到的是这个对象的引用。这个对象的任何变化，都会反映到目标对象上面





# 数值的扩展

**指数运算符**

ES2016 新增了一个指数运算符（**）

~~~js
2 ** 2; // 4
2 ** 3; // 8
2 ** 3 ** 2; // 512  相当于=>  2 ** (3 ** 2)
~~~

这个运算符的一个特点是右结合，而不是常见的左结合。多个指数运算符连用时，是从最右边开始计算的

指数运算符可以与等号结合，形成一个新的赋值运算符（**=）

~~~js
let a = 1.5;
a **= 2;
// 等同于 a = a * a;
let b = 4;
b **= 3;
// 等同于 b = b * b * b;
~~~





# 函数的扩展

## 默认参数

ES6 之前，不能直接为函数的参数指定默认值，只能采用变通的方法

~~~js
function fn(a, b) {
  b = b || 2;
  console.log(a, b);
}
fn(1); // 1 2
~~~



ES6 允许为函数的参数设置默认值，即直接写在参数定义的后面

~~~js
function fn(a, b = 2) {
  console.log(a, b);
}

fn(1); // 1 2
fn(1, 3); // 1 3
~~~

~~~js
function Point(a = 0, b = 0) {
  this.a = a;
  this.b = b;
}

const p = new Point();
p; // { a: 0, b: 0 }
~~~



参数变量是默认声明的，所以不能用`let`或`const`再次声明

~~~js
function fn(a = 3) {
  let a = 1; // 报错
  const a = 2; // 报错
}
~~~



与解构赋值默认值结合使用

```javascript
function fn({a, b = 5}) {
  console.log(a, b);
}

fn({}); // undefined 5
fn({a: 1}); // 1 5
fn({a: 1, b: 2}); // 1 2
fn(); // 报错
```

```javascript
function fn({a, b = 5} = {}) {
  console.log(a, b);
}

fn(); // undefined 5
```



**参数默认值位置**

通常情况下，定义了默认值的参数，应该是函数的尾参数

```javascript
function fn(a = 1, b) {
  return [a, b];
}

fn(); // [1, undefined]
fn(2); // [2, undefined])
fn(, 1); // 报错
fn(undefined, 1); // [1, 1]
```

上面代码中，有默认值的参数都不是尾参数。这时，无法只省略该参数，而不省略它后面的参数，除非显式输入`undefined`

如果传入`undefined`，将触发该参数等于默认值，`null`则没有这个效果

```javascript
function fn(a = 5, b = 6) {
	console.log(a, b);
}

fn(undefined, null)
// 5 null
```

上面代码中，`x`参数对应`undefined`，结果触发了默认值，`y`参数等于`null`，就没有触发默认值



## rest 参数

ES6 引入 `rest `参数（形式为…变量名），用于获取函数的多余参数，这样就不需要使用 arguments 对象了。rest 参数搭配的变量是一个数组，该变量将多余的参数放入数组中

~~~js
function add(...values) {
 let sum = 0;
 for (let val of values) {
   sum += val;
 }
 return sum;
}
add(2, 5, 3); // 10
~~~

~~~js
function add(a, ...values) {
 let sum = 0;
 for (let val of values) {
   sum += val;
 }
 return sum;
}
add(2, 5, 3); // 8   因为a = 2, ...values = [5, 3]
~~~

上面代码的 add 函数是一个求和函数，利用 rest 参数，可以向该函数传入任意数目的参数。

注意，**rest 参数之后不能再有其他参数**（即只能是最后一个参数），否则会报错

~~~js
// 报错
function fn(a, ...b, c) {
	// ...
}
~~~



## 箭头函数（ES6）

### 箭头函数语法

总结：

箭头函数相当于匿名函数，所以需要变量接收

如果参数只有一个，不需要括号，参数没有或者多个则需要括号

如果代码块部分多于一条语句，需要大括号{}

如果需要返回一个对象，必须在对象外面加上括号



~~~js
var f = () => 'hello'

// 等同于
var f = () => { return 'hello' }

// 等同于
var f = function() { return 'hello' }
~~~

~~~js
// ES5
var f = function(a, b) { return a * b };

// ES6
var f = (a, b) => a * b;
~~~



当箭头函数只有一个参数时，可以省略括号，直接写参数名

~~~js
var f = a => a;
~~~



当箭头函数没有参数或者多个参数是，不能省略括号

~~~js
var f = () => 'hello';
~~~

~~~js
var sum = (a, b) => a + b;
~~~



当箭头函数的代码块部分多于一条语句，就要使用 `{}` 将它们括起来，并且使用 `return` 语句返回

~~~js
var sum = (a, b) => { 
  console.log('hello');
  return a + b; 
}
sum(1, 2);
// hello
// 3
~~~



由于大括号被解释为代码块，所以如果箭头函数直接返回一个对象，必须在对象外面加上括号，否则会报错

```javascript
let getObj = id => ({ id: id, name: 'aaa' });
```



### 箭头函数示例

箭头函数可以与变量解构结合使用

```javascript
const getName = ({ first, last }) => first + ' ' + last;

// 等同于
function getName(person) {
  return person.first + ' ' + person.last;
}
```



箭头函数使得表达更加简洁。

```javascript
const iseven = n => n % 2 === 0
const square = n => n * n
```



箭头函数的一个用处是简化回调函数。

```javascript
// 正常函数写法
[1, 2, 3].map(function(i) { 
    return i * i;
})

// 箭头函数写法
[1, 2, 3].map(i => i * i);
```

另一个例子是

```javascript
// 正常函数写法
var res = arr.sort(function(a, b) {
  return a - b;
})

// 箭头函数写法
var res = arr.sort((a, b) => a - b);
```



下面是 rest 参数与箭头函数结合的例子

```javascript
const f = (...a) => a;

f(1, 2, 3, 4, 5)
// [1, 2, 3, 4, 5]

const f = (a, ...b) => [a, b];

fn(1, 2, 3, 4, 5)
// [1, [2, 3, 4, 5]]
```



注意: 函数体内的 this 对象，就是定义时所在的对象，而不是使用时所在的对象

`this` 对象的指向是可变的，但是在箭头函数中，它是固定的

~~~js
function foo() {
  setTimeout(() => {
    console.log('id:', this.id);
  }, 100);
}
let id = 21;
foo.call({ id: 42 });
// id: 42
~~~

上面代码中，setTimeout 的参数是一个箭头函数，这个箭头函数的定义生效是在 foo 函数生成时，而它的真正执行要等到 100 毫秒后。如果是普通函数，执行时 this 应该指向全局对象window，这时应该输出 21。但是，箭头函数导致 this 总是指向函数定义生效时所在的对象（本例是{ id: 42}），所以输出的是 42。



### 箭头函数特性

~~~js
* 没有 this  super  arguments
* 不可以当作构造函数，也就不能通过 new 关键字调用
* 没有原型属性 prototype
* 不可以改变 this 指向
* 不支持重复的命名参数

注意：箭头函数和传统函数一样都有一个 name 属性，这一点是不变的
~~~

**`this指向的固定化，并不是因为箭头函数内部有绑定this的机制，实际原因是箭头函数根本没有自己的this，导致内部的this就是外层代码块的this。正是因为它没有this，所以也就不能用作构造函数`**



**箭头函数没有this，只能从上下文获取this**

箭头函数的`this`值，取决于函数外部非箭头函数的`this`值，如果上一层还是箭头函数，那就继续往上找，如果找不到那么`this`就是`Window`对象

~~~js
var person = {
    f1: () => {
        console.log(this)
    },
    f2: function() {
        return () => { console.log(this) }
    }
}
person.f1();  // Window
person.f2()();  // person对象
~~~



**箭头函数没有arguments对象**

箭头函数也没有`arguments`对象，但是如果它外层还有一层非箭头函数的话，就会去找外层的非箭头函数的`arguments`对象，注意：箭头函数找arguments对象只会找外层非箭头函数的函数，如果外层是一个非箭头函数的函数如果它也没有arguments对象也会中断返回，就不会在往外层去找了，如下

~~~js
var f1 = () => console.log(arguments);  // 执行该函数会抛出错误

function f2(a, b, c) {
    return () => {
        console.log(arguments); // [1, 2, 3]
    }
}
f2(1, 2, 3)();
~~~

可以清楚的看到当前的箭头函数没有`arguments`对象，然而就去它的外层去找非箭头函数的函数。``

~~~js
function fn(a) {
    return function() {
        return () => {
            console.log(arguments); // []
        }
    }
}
fn(1)()();
~~~

上面示例中可以看到，里面的箭头函数往外层找非箭头函数的函数，然后不管外层这个函数有没有`arguments`对象都会返回。只要它是非箭头函数就可以，如果外层是箭头函数还会继续往外层找

~~~js
var f = (...a) => console.log(a);
f(1, 2, 3); // [1, 2, 3]
~~~



**箭头函数不能用`new`关键字声明**

~~~js
var Fn = () => {};
new Fn(); // 抛出错误，找不到constructor对象
~~~



**箭头函数没有原型`prototype`**

箭头函数没有原型，有可能面试官会问，`JavaScript`中所有的函数都有`prototype`属性吗

~~~js
var fn = () => {};
fn.prototype; // undefined
~~~



**箭头函数不能改变`this`指向**

~~~js
var person = {};
var fn = () => console.log(this);

fn.bind(person)(); // Window (不是person)
fn.call(person); // Window (不是person)
fn.apply(person); // Window (不是person)
~~~



### 箭头函数和普通函数的区别

~~~js
* 相比普通函数, 箭头函数有更简洁的语法
* 箭头函数不绑定 this ，会捕获其所在的上下文的 this 值，作为自己的 this 值
* 箭头函数是匿名函数, 不能作为构造函数，不可以使用 new 命令，否则会抛出一个错误
* 箭头函数没有 arguments，取而代之用 rest参数...解决
* 箭头函数的 this 永远指向其上下文的 this ，任何方法都改变不了其指向，如 call()、bind()、apply() ，可以说正是因为没有自己的 this
* 箭头函数没有原型属性 prototype
~~~









# Set

> ES6 提供了新的数据结构 Set，它类似于数组，但是成员的值都是唯一的，没有重复的值

Set 本身是一个构造函数，用来生成 Set 数据结构（既然是构造函数，肯定需要new）

~~~js
const s = new Set();
[2, 3, 5, 4, 5, 2, 2].forEach(i => s.add(i));
for(let i of s) {
	console.log(i);
}
// 2 3 5 4
~~~

去除数组的重复成员

~~~js
const set = new Set([1, 2, 3, 4, 4]);
[...set];
// [1, 2, 3, 4]
~~~

或者

~~~js
const arr = [1, 1, 2, 3, 4, 4];
[...new Set(arr)];
// [1, 2, 3, 4]
~~~

或者

~~~js
const arr = [1, 1, 2, 3, 4, 4];
Array.from(new Set(arr));
// [1, 2, 3, 4]
~~~





# Map

Map 数据结构类似于对象，是键值对的集合，传统的键只能用字符串，Map 的键不限于字符串，各种类型的值（包括对象）都可以当作键。
属性和操作方法

~~~js
size 属性，返回 Map 结构的成员总数
set(key,value)方法，设置set方法设置键名key对应的键值为value，然后返回整个 Map 结构。如果key已经有值，则键值会被更新，否则就新生成该
get(key) 方法，读取key对应的键值，如果找不到key，返回undefined
has(key) 方法，返回一个布尔值，表示某个键是否在当前 Map 对象之中。
delete(key) 方法，删除某个键，返回true。如果删除失败，返回false。
clear(key) 方法，清除所有成员，没有返回值。
~~~

Map 遍历

~~~js
keys() // 返回键名的遍历器
values() // 返回键值的遍历器
entries() // 返回所有成员的遍历器
forEach() // 遍历Map的所有成员
~~~





# Promise 教程

## Promise 实例对象

> Promise 是异步编程的一种解决方案 ，比传统的解决方案（回调函数和事件）更合理和更强大 

 所谓Promise，简单说就是一个容器，里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果



**Promise对象特点**

	（1）Promise对象可以保存异步操作的结果
	（2）Promise异步操作具有三种状态，Pending、Resolved 和 Rejected
	（3）Promise对象状态的改变只存在两种情况，Pending 到 Resolved 或者 Pending 到 Rejected
	（4）Promise对象的状态一旦确定，那么就无法改变，要么是 Resolved，要么是 Rejected

**特别说明**：Pending表示等待状态，Resolved表示处于完成状态，Rejected处于未完成状态

既然Promise创建的实例对象，是一个异步操作，那么异步操作的结果，只能有两种状态：

​		状态1：异步执行成功，需要在内部调用成功的回调函数`resolve`把结果返回给调用者

​		状态2：异步操作失败，需要在内部调用失败的回调函数`reject` 把结果返回给调用者



**基本用法**

~~~js
let p = new Promise((resolve, reject) => {
    if (异步操作成功) {
        resolve(value)	// 异步操作成功，就会调用这个回调函数，并把异步成功的结果当做参数
    } else {
        reject(error)	// 异步操作失败，就会调用这个回调函数，并把异步失败的结果当做参数
    }
})
~~~

简单分析：

（1）通过构造函数`new Promise()`可以创建一个Promise对象实例，构造函数的参数是一个回调函数

（2）构造函数的回调函数具有两个函数参数，由引擎提供，也就是不需要我们提供

（3）执行resolve函数，那么状态变为Resolved，执行reject函数，状态变为Rejected

（4）构造函数调用后，回调函数会**立马执行**，然后根据调用的是resolve还是reject函数，确定状态

（5）状态确定后，再利用then方法执行对应的操作

~~~js
p.then((value) => {
	console.log(value)  // 这个value就是resolve(value)的参数value
}, (error) => {
    console.log(error)  // 这个error就是reject(error)的参数error
});
~~~

简单分析：

（1）.then方法的参数是两个回调函数

（2）如果p处于Resolved完成状态，那么执行第一个回调函数，如果处于Rejected状态，那么执行第二个回调函数

（3）回调函数中的参数value，分别是传递给resolve和reject函数的参数

（4） 第二回调函数是可以省略的 



**Promise示例**

~~~js
const p = new Promise(function(resolve, reject) {
    setTimeout(function() {
        resolve('hello')
    }, 5000)
})
p.then(function(value) {
    console.log(value)
})
// 5秒后输出 hello
~~~



~~~js
function getHello(ms) {
    return new Promise((resolve, reject) => {
        setTimeout(resolve, ms, 'hello') // setTimeout(函数, 延时时间ms, 参数)
    })
}

getHello(5000).then((value) => { // 5s后输出hello  getHello(5000)=>返回一个实例对象
    console.log(value)
})
// 5秒后输出 hello
~~~



~~~js
const p = new Promise((resolve, reject) => {
  console.log(1);
  resolve();
  console.log(2)
});

p.then(function() {
  console.log(3);
});

console.log(4);

// 1 2 4 3
~~~



上面代码中， Promise 新建后立即执行 ，首先输出1，然后，then方法指定的回调函数，将在当前脚本所有同步任务执行完才会执行，所以resolved最后输出。



resolve回调函数的参数除了正常的值以外，还可以返回另外一个Promise实例对象

~~~js
const p1 = new Promise((res, rej) => {
    setTimeout(() => rej(new Error('失败')), 3000)
})

const p2 = new Promise((res, rej) => {
    setTimeout(() => res(p1), 1000)
})

p2.then(value => console.log(value), error => console.log(error)) // 3s后输出 Error: 失败
~~~

上面代码中，p1是一个 Promise，3 秒之后变为rejected。p2的状态在 1 秒之后改变，resolve方法返回的是p1。由于p2返回的是另一个 Promise，导致p2自己的状态无效了，由p1的状态决定p2的状态。所以，后面的then语句都变成针对后者（p1）。又过了 2 秒，p1变为rejected，导致触发catch方法指定的回调函数。



**注意点**

~~~js
new Promise((resolve, reject) => {
	resolve(1);
	console.log(2);
}).then(v => {
	console.log(v);
});
// 2
// 1
~~~

 一般来说，调用`resolve`或`reject`以后，Promise 的使命就完成了，后继操作应该放到`then`方法里面，而不应该直接写在`resolve`或`reject`的后面。所以，最好在它们前面加上`return`语句，这样就不会有意外 

~~~js
new Promise((resolve, reject) => {
	return resolve(1);
	// 后面的语句不会执行
	console.log(2);
})
~~~



## .then() 方法

**`只要是Promise实例对象就能调用then方法`**

~~~js
p.then(onResolved, onRejected)

// onResolved：必需，当Promise对象变为 Resolved 状态时的回调函数
// onRejected：可选，当Promise对象变为 Rejected 状态时的回调函数
~~~

Promise 实例对象具有then方法，也就是说，then方法是定义在原型对象Promise.prototype上的

调用then方法，预先为这个Promise异步操作，指定成功(resolve)和失败(reject)回调函数



~~~js
let p = new Promise((resolve, reject) => {
if (true) {
    resolve('resolve被调用');
  } else {
    reject('reject被调用');
  }
});
 
p.then((res) => { console.log(res)}, (err) => { console.log(err) })
// resolve被调用
~~~

分析：

调用Promise构造函数后，其回调函数会立马被调用

通过if语句判断之后，resolve()会被调用，于是Promise对象状态变为Resolved

于是就会执行then的第一个回调函数，打印结果是"resolve被调用"



**then()方法返回一个promise对象，所以可以使用链式调用方式**

~~~js
let p = new Promise((resolve, reject) => {
    resolve('hello')
})
p.then((res) => {
    console.log(res);
    return `${res} world`
}).then((res) => {
    console.log(res);
})
// hello
// hello world
~~~

分析：

上述代码中，第二个then()方法的回调函数的参数是上一个then回调函数的返回值



then方法返回的是一个新的Promise实例（注意，不是原来那个Promise实例）。因此可以采用链式写法，即then方法后面再调用另一个then方法。

~~~js
new Promise((res, rej) => {
    setTimeout(res, 3000, 'hello')
}).then(v => v).then((r) => console.log(r)) // 3s后输出hello
~~~

上面代码，可以看出，第二then的成功回调函数参的数，其实就是第一个then成功回调函数return返回的值，也就是说第一个then返回的值当做第二then的参数



## .catch() 方法

~~~js
p.catch(onRejected);

// onRejected：必需，当 p 的状态变为 Rejected 时，此回调函数就会执行
~~~



~~~js
Promise.prototype.catch()方法是
.then(null, reject)
或
.then(undefined, reject) 的别名，用于指定发生错误时的回调函数
~~~

下面代码中， 

如果该对象状态变为`resolved`，则会调用`then()`方法指定的回调函数

如果异步操作抛出错误，状态就会变为`rejected`，就会调用`catch()`方法指定的回调函数，处理这个错误

另外，`then()`方法指定的回调函数，如果运行中抛出错误，也会被`catch()`方法捕获。

~~~js
p
.then((value) => console.log('成功：', value))
.catch((error) => console.log('失败：', error))
~~~

上面代码等同于：

~~~js
p
.then((value) => console.log('成功：', value))
.then(null, (error) => console.log('失败：', error))
~~~

示例

~~~js
const p = new Promise((res, rej) => {
    throw new Error('错误')
})
p.catch((error) => {
    console.log(error)
})
// Error: 错误
~~~

 上面代码中，`promise`抛出一个错误，就被`catch()`方法指定的回调函数捕获。注意，上面的写法与下面两种写法是等价的。 

~~~js
// 写法一
const p = new Promise((resolve, reject) => {
  try {
    throw new Error('错误')
  } catch(e) {
    reject(e)
  }
})
p.catch((error) => {
  console.log(error) // Error: 错误
})

// 写法二
const p = new Promise((resolve, reject) => {
  reject(new Error('错误'))
})
p.catch((error) => {
  console.log(error) // Error: 错误
})
~~~

 比较上面两种写法，可以发现`reject()`方法的作用，等同于抛出错误。 

 如果 Promise 状态已经变成`resolved`，再抛出错误是无效的。 

~~~js
const p = new Promise((resolve, reject) => {
  resolve('yes');
  throw new Error('no');
});
p
.then((res) => { console.log(res) })
.catch((err) => { console.log(err) })
// yes
~~~

 上面代码中，Promise 在`resolve`语句后面，再抛出错误，不会被捕获，等于没有抛出。因为 Promise 的状态一旦改变，就永久保持该状态，不会再变了。



~~~js
let p = new Promise(function(resolve, reject) {
  if (false) {
    resolve()
  } else {
    reject()
  }
})
 
p
.then(function () {
  console.log('异步成功')
})
.catch(function () {
  console.log('异步失败')
})
// 异步失败
~~~

或者

~~~js
let p = new Promise(function(resolve, reject) {
  if (false) {
    resolve()
  } else {
    reject()
  }
})
 
p
.then(function () {
  console.log('异步成功')
}, function() {
  console.log('异步失败')
})
// 异步失败
~~~

或者

~~~js
let p = new Promise(function(resolve, reject) {
  if (false) {
    resolve()
  } else {
    reject()
  }
})
 
p
.then(function () {
  console.log('异步成功')
})
.then(() => {}, () => { console.log('异步失败') })
// 异步失败
~~~



**catch()可以捕获它之前Rejected状态变化，不必紧邻**

~~~js
let p = new Promise(function(resolve, reject) {
  reject()
});
 
p.
then(function () {
  //code
})
.then(function () {
  //code
})
.catch(function () {
  console.log("错误失败")
})
// 错误失败
~~~

 

## .all() 方法

等待所有都完成（或第一个失败）

~~~js
const p1 = Promise.resolve(3);
const p2 = 100;
const p3 = new Promise((resolve, reject) => {
  setTimeout(resolve, 100, 'ok');
});

Promise.all([p1, p2, p3]).then((values) => {
  console.log(values); // [3, 100, "ok"]
});
~~~



Promise.all 可以将多个Promise实例包装成一个新的Promise实例。同时，成功和失败的返回值是不同的，成功的时候返回的是一

个结果数组，而失败的时候则返回最先被reject失败状态的值

~~~js
let p1 = new Promise((resolve, reject) => {
  resolve('p1_success')
})

let p2 = new Promise((resolve, reject) => {
  resolve('p2_success')
})

let p3 = Promise.reject('p3_fail')

Promise.all([p1, p2]).then((res) => {
  console.log(res)  // ['p1_success', 'p2_success']
}).catch((error) => {
  console.log(err)
})

Promise.all([p1, p3 ,p2]).then((res) => {
  console.log(res)
}).catch((err) => {
  console.log(err)      // 'p3_fail'
})
~~~



~~~js
let wake = (time) => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(`${time / 1000}秒后醒来`)
    }, time)
  })
}

let p1 = wake(3000)
let p2 = wake(2000)

Promise.all([p1, p2]).then((res) => {
  console.log(res)       // [ '3秒后醒来', '2秒后醒来' ]
}).catch((err) => {
  console.log(err)
})
~~~

**需要特别注意的是，Promise.all获得的成功结果的数组里面的数据顺序和Promise.all接收到的数组顺序是一致的，即p1的结果在前，即便p1的结果获取的比p2要晚。**



## .race() 方法

顾名思义，Promse.race就是赛跑的意思，意思就是说，Promise.race([p1, p2, p3])里面哪个结果获得的快，就返回那个结果，不管

结果本身是成功状态还是失败状态

~~~js
let p1 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('success')
  },1000)
})

let p2 = new Promise((resolve, reject) => {
  setTimeout(() => {
    reject('failed')
  }, 500)
})

Promise.race([p1, p2]).then((res) => {
  console.log(res)
}).catch((err) => {
  console.log(err)  // 打开的是 'failed'
})
~~~



## 解决回调地狱

~~~js
function getFileByPath(path) {
    return new Promise(function(resolve, reject) {
        fs.readFile(path, 'utf-8', (error, data) => {
            if(error) return reject(error)
            resolve(data)
        })
    })
}

// .then先执行
getFileByPath('./files/02.txt').then(
function(data) {
    console.log(data)
}, 
funtion(error) {
    console.log(error) 
})
~~~

解决回调地狱

~~~js
getFileByPath('./files/01.txt')
.then(function(data) {
    console.log(data)
    return getFileByPath('./files/02 .txt')
})
.then(function(data2) {
    console.log(data2)
    return getFileByPath('./files/03 .txt')
})
.then(function(data3) {
    console.log(data3)
})
~~~

如果前面的Promise执行失败，我们不想让后续的Promise被终止，可以为每个Promise指定失败回调

~~~js
getFileByPath('./files/01.txt')
.then(function(data) {
    console.log(data)
    return getFileByPath('./files/02 .txt')
}, function(error) {
    console.log(error)
    return getFileByPath('./files/02 .txt')
})
.then(function(data2) {
    console.log(data2)
})
~~~

有时候，我们有这样的需求，如果后续Promise执行，依赖于前面Promise执行的结果，如果前面失败了， 则后面的就没有执行下去的意义了，此时我们想要实现，一旦报错，则立即终止所有Promise的执行

~~~js
getFileByPath('./files/01.txt')
.then(function(data) {
    console.log(data)
    return getFileByPath('./files/02 .txt')
})
.then(function(data2) {
    console.log(data2)
    return getFileByPath('./files/03 .txt')
})
.then(function(data3) {
    console.log(data3)
})
.catch(function(error) {
    console.log(error)
})
// 如果前面有任何的promise执行失败，会立即终止所有promise，并马上进入catch去处理promise中抛出的异常
~~~



~~~js
const someAsyncThing = function(flag) {
	return new Promise(function(resolve, reject) {
		if(flag){
			resolve('ok');
		}else{
			reject('error')
		}
	});
};

someAsyncThing(true).then((data)=> {
	console.log('data:',data); // 输出 'ok'
}).catch((error)=>{
	console.log('error:', error); // 不执行
})

someAsyncThing(false).then((data)=> {
	console.log('data:',data); // 不执行
}).catch((error)=>{
	console.log('error:', error); // 输出 'error'
})
~~~

上面代码中，someAsyncThing 函数成功返回 ‘OK’, 失败返回 ‘error’, 只有失败时才会被 catch 捕捉到。



# async/await异步操作

## 含义

> ES2017 标准引入了 async 函数，使得异步操作变得更加方便

async 函数是什么？一句话，它就是 Generator 函数的语法糖

`async/await`从字面意思上很好理解，`async`是异步的意思，`await`有等待的意思，而两者的用法上也是如此。`async`用于申明一个`function`是异步的，而`await` 用于等待一个异步方法执行完成。

`async` 函数的使用方式，直接在普通函数前面加上 `async`，表示这是一个异步函数，在要异步执行的语句前面加上 `await`，表示后面的表达式需要等待



## 基本用法

### async关键词

async的语法很简单，就是在函数开头加一个`async`关键字，示例如下：

~~~js
function f1() {
    return 1;
}

async function f2() {
    return 1;
}

console.log(f1()) // 1
console.log(f2()) // Promise{<fulfilled>:1}
~~~

**凡是在前面添加了async的函数在执行后都会自动返回一个Promise对象**

async函数会返回一个promise对象，如果function中返回的是一个值，async直接会用Promise.resolve()包裹一下返回：

~~~js
async function f2() {
    return 1;
}

async function f2() {
    return Promise.resolve(1);
}

async function f2() {
    return await 1;
}

// 上面3个函数作用等同

f2().then((res) => {
    console.log(res) // 1
})
~~~



### await关键词

关键词`await`是等待的意思，其后面是一个表达式，这个表达式可以是常量、变量、Promise以及函数等

**await必须在async函数里使用，不能单独使用**

**await后面需要跟Promise对象，不然就没有意义，而且await后面的Promise对象不必写then，因为await的作用之一就是获取后面Promise对象成功状态传递出来的参数**

`await`操作符等的是一个返回的结果，那么如果是同步的情况，那就直接返回了

异步的情况下，`await`会阻塞整一个流程，直到结果返回之后，才会继续下面的代码

~~~js
function f1() {
    return 'aaa';
}

async function f2() {
    return Promise.resolve('bbb');
}

async function test() {
    const a = await f1();
    const b = await f2();
    console.log(a, b);
}

test(); // aaa bbb
~~~

>阻塞代码是一个很可怕的事情，而async函数，会被包在一个promise中，异步去执行。所以await只能在async函数中使用，如果在正常程序中使用，会造成整个程序阻塞，得不偿失。



###  基本示例

当函数执行的时候，一旦遇到`await`就会先返回，等到异步操作完成，再接着执行函数体内后面的语句

~~~js
function timeout(ms) {
    return new Promise((res) => {
        setTimeout(res, ms)
    })
}

async function asyncFn(v, ms) {
    await timeout(ms) // 必须等待await后面表达式成功返回才会执行后面语句
    console.log(v)
}

asyncFn('hello', 5000) // 5s后输出hello
~~~

 正常情况下，`await`命令后面是一个 Promise 对象，返回该对象的结果。如果不是 Promise 对象，就直接返回对应的值

~~~js
async function f() {
  return await 'hello'; // 等同于 return 'hello';
}

f().then(v => console.log(v)) // hello 【then的回调函数的接收的值是return语句返回的await语句返回值】
~~~

~~~js
async function f() {
  throw new Error('出错了');
}

f().then(
  v => console.log(v),
  e => console.log(e) // Error: 出错了
)

---------------------------------

async function f() {
  await Promise.reject('出错了');
}

f().then(
  v => console.log(v),
  e => console.log(e) // 出错了
)

---------------------------------

async function f() {
  await Promise.reject('出错了');
}

f()
.then(v => console.log(v))
.catch(e => console.log(e)) // 出错了
~~~

 注意，上面代码中，`await`语句前面没有`return`，但是`reject`方法的参数依然传入了`catch`方法的回调函数。这里如果在`await`前面加上`return`，效果是一样的。 

如果await后面的Promise变为reject状态，则reject的参数会被catch回调函数接收

**如果是变为reject状态，前面不加return，reject的参数也会被catch回调函数接收**

~~~js
async function f() {
  await Promise.reject('错误');
  await 10;
  console.log('hello')
}
f().then((res) => { console.log(res) }, (err) => { console.log(err) })
// 错误 【抛出错误后，会中断整个async函数的执行】
~~~



## 错误处理

任何一个`await`语句后面的 Promise 对象变为`reject`状态，那么整个`async`函数都会中断执行。 

~~~js
async function f() {
  await Promise.reject('出错了');
  await Promise.resolve('hello world'); // 不会执行
}
f()
~~~

 上面代码中，第二个`await`语句是不会执行的，因为第一个`await`语句状态变成了`reject`。

 有时候，我们希望即使前一个异步操作失败，也不要中断后面的异步操作。这时可以将第一个`await`放在`try...catch`结构里面，这样不管这个异步操作是否成功，第二个`await`都会执行。 

~~~js
async function f() {
  try {
    await Promise.reject('出错了');
  } catch(e) {
    console.log(e); // 出错了
  }
  return await Promise.resolve('hello');
}

f().then(v => console.log(v))
// hello
~~~

 另一种方法是`await`后面的 Promise 对象再跟一个`catch`方法，处理前面可能出现的错误。 

~~~js
async function f() {
  await Promise.reject('出错了').catch(e => console.log(e));
  return await Promise.resolve('hello world');
}

f().then(v => console.log(v))
// 出错了
// hello world
~~~

 

promise并不是只有一种resolve，还有一种reject的情况。而await只会等待一个结果，发生错误了有以下方式捕捉：

**用try-catch来做错误捕捉**

~~~js
async function f() {
    try {
        await Promise.reject('error')
    } catch (err) {
        console.log(err)
    }
}

f() // error
~~~

~~~js
async function f() {
  try {
    await Promise.reject('失败');
  } catch(e) {
  }
  return await Promise.resolve('成功');
}
f()
.then((res) => {
  console.log('res ' + res)
})
.catch((err) => {
    console.log('err ' + err)
})
// res 成功
// 可以将可能抛出错误的语句放入try catch语句中
~~~



~~~js
async function f() {
  await Promise.reject('失败').catch((err) => { console.log(err) });
  return await Promise.resolve('成功');
}
f()
.then((res) => {
  console.log(res)
})
// 失败 成功
// 也可以在可能抛出错误的promise对象后面使用catch来捕获抛出的错误
~~~

~~~js
async function func() {
  try {
    var res1 = await a();
    var res2 = await b();
    var res3 = await c();
  }
  catch (err) {
    console.error(err);
  }
}
// 如果有多个await语句，那么可以将其统一放在try语句中
// 特别说明：如果具有多个await语句，且它们之间不是继发关系，建议让它们同时触发，以达到最大性能
~~~



## 继发并发

如果具有多个await语句，且它们之间不是继发关系，建议让它们同时触发，以达到最大性能

getA和getB是独立的异步操作，没必要是继发关系，也就是执行完a再去执行b，那么可以采用以下方式

~~~js
let [a, b] = await Promise.all([getA(), getB()]);
~~~

或者

~~~js
let aPromise = getA();
let bPromise = getB();
let a = await aPromise();
let b = await bPromise();
~~~



## 优点

在我们处理异步的时候，比起回调函数，Promise的then方法会显得较为简洁和清晰，但是在处理多个**彼此之间相互依赖的请求的时候**，就会显的有些累赘。这时候，用async和await更加优雅



# Module 的语法

~~~js
// CommonJS模块
let { a, b, c } = require('fs');

// 等同于
let _fs = require('fs');
let a = _fs.a;
let b = _fs.b;
let c = _fs.c;
~~~

## 严格模式

ES6 的模块自动采用严格模式，不管你有没有在模块头部加上`"use strict";`。

严格模式主要有以下限制：

- 变量必须声明后再使用
- 函数的参数不能有同名属性，否则报错
- 不能使用`with`语句
- 不能对只读属性赋值，否则报错
- 不能使用前缀 0 表示八进制数，否则报错
- 不能删除不可删除的属性，否则报错
- 不能删除变量`delete prop`，会报错，只能删除属性`delete global[prop]`
- `eval`不会在它的外层作用域引入变量
- `eval`和`arguments`不能被重新赋值
- `arguments`不会自动反映函数参数的变化
- 不能使用`arguments.callee`
- 不能使用`arguments.caller`
- 禁止`this`指向全局对象
- 不能使用`fn.caller`和`fn.arguments`获取函数调用的堆栈
- 增加了保留字（比如`protected`、`static`和`interface`）

## import 和 export

**导出 export**

~~~js
// moudle.js
export var num = 10;
export var obj = { name: 'hello' };
export function fn(v) {
	console.log(v)
};
~~~

或者（推荐）

~~~js
// moudle.js
var num = 10;
var obj = { name: 'hello' };
function fn(v) {
	console.log(v)
};
export { num, obj, fn }
~~~

**导入 import**

~~~js
// main.js
import { num, obj, fn } from './moudle.js';

fn(num); // 10
num = 20; // 报错，import 命令输入的变量都是只读的
obj.name = 'hi'; // ok，如果变量是一个对象，改写变量的属性是允许的
~~~



 **别名**

通常情况下，`export`输出的变量就是本来的名字，但是可以使用`as`关键字重命名

```javascript
var a1 = 10
var a2 = 20

export { a1 as a, a2 as b };
```

~~~js
import { a1 as a } from './moudle.js';
~~~



**注意写法**

变量

```javascript
export 1; // 报错

var a = 1;
export a; // 报错，没有声明变量
```

```javascript
// 写法一
export var a = 1;

// 写法二
var a = 1;
export { a };

// 写法三
var a = 1;
export { a as b };
```

方法

```javascript
// 报错
function fn() {}
export fn;

// 正确
export function fn() {};

// 正确
function fn() {}
export { fn };
```



**export 导出命令**

​		一个模块就是一个独立的文件，该文件内部的所有变量，外部无法获取。如果你希望外部能够读取模块内部的某个变量，就必须使用`export`关键字输出该变量。ES6 将`moudle.js`其视为一个模块，里面用`export`命令对外部输出了三个变量。

另外，`export`语句输出的接口，与其对应的值是动态绑定关系，即通过该接口，可以取到模块内部实时的值。

```javascript
export var foo = 'bar';

setTimeout(() => foo = 'baz', 500);
```

上面代码输出变量`foo`，值为`bar`，500 毫秒之后变成`baz`。

最后，`export`命令可以出现在模块的任何位置，只要处于模块顶层就可以。如果处于块级作用域内，就会报错，下一节的`import`命令也是如此。这是因为处于条件代码块之中，就没法做静态优化了，违背了 ES6 模块的设计初衷。

```javascript
function fn() {
  export default 'bar' // error
}

fn()
```

上面代码中，`export`语句放在函数之中，结果报错



**import导入命令**

`import`命令接受一对大括号，里面指定要从其他模块导入的变量名。大括号里面的变量名，必须与被导入模块（`moudle.js`）对外接口的名称相同。

* 由于`import`是静态执行，所以不能使用表达式和变量。

* `import`命令具有提升效果，会提升到整个模块的头部，首先执行

~~~js
fn();

import { fn } from './moudle.js';
~~~

上面的代码不会报错，因为`import`的执行早于`foo`的调用。这种行为的本质是，`import`命令是编译阶段执行的，在代码运行之前



## 模块的整体加载

除了指定加载某个输出值，还可以使用整体加载，即用星号（`*`）指定一个对象，所有输出值都加载在这个对象上面

```javascript
// moudle.js
export function add(a, b) {
  return a + b;
}

export function reduce(a, b) {
  return a - b
}
```

**普通加载**

```javascript
// main.js
import { add, reduce } from './moudle.js';

add(3, 2) // 5
reduce(3, 2) // 1
```

**整体加载**

```javascript
// main.js
import * as com from './moudle.js';

com.add(3, 2); // 5
com.red(3, 2); // 1
```



## export default

`export default`命令，为模块指定默认输出

```javascript
// moudle.js

export default function() {
  console.log('hello');
}
```

其他模块加载该模块时，`import`命令可以为该匿名函数指定任意名字

```javascript
// main.js
import sayHello from './moudle.js';

sayHello(); // hello
```

需要注意的是，这时`import`命令后面，**不使用大括号**



`export default`命令用在非匿名函数前，也是可以的

```javascript
export default function sayHello() {
  console.log('hello');
}

// 或者写成
function sayHello() {
  console.log('hello');
}

export default sayHello;
```

上面代码中，`sayHello`函数的函数名`sayHello`，在模块外部是无效的，加载的时候，视同匿名函数加载

```javascript
// moudle.js
function add(a, b) {
  return a + b;
}
export { add as default }; // 等同于 export default add;

// main.js
import { default as foo } from './moudle.js'; // 等同于 import foo from './modules.js';
```

正是因为`export default`命令其实只是输出一个叫做`default`的变量，所以它后面不能跟变量声明语句

```javascript
// ok
export var a = 1;

// ok
var a = 1;
export default a;

// error
export default var a = 1;
```

同样地，因为`export default`命令的本质是将后面的值，赋给`default`变量，所以可以直接将一个值写在`export default`之后

```javascript
// ok
export default 99;

// error
export 99;
```

上面代码中，后一句报错是因为没有指定对外的接口，而前一句指定对外接口为`default`



> **总结**

~~~js
1. 当用 export default 导出时，就用 import 导入（不带大括号）

2. 一个文件里，有且只能有一个 export default ，但可以有多个 export

3. 当用 export a 时，就用 import { a } 导入（记得带上大括号）

4. 当一个文件里，既有一个 export default people, 又有多个 export name 或者 export age 时，导入就用
	import people, { name, age } from './moudle.js';

5. 当一个文件里出现 n 多个 export 导出很多模块，导入时除了一个一个导入，也可以用
  import * as com from './moudle.js';
~~~





# class 基本语法

**基本用法**

ES5

~~~js
function Person(name, age) {
  this.name = name;
  this.age = age;
}

Person.prototype.say = function() {
  console.log(this.name, this.age);
};

const p = new Person('Jack', 18);
p.say(); // Jack 18
~~~

ES6

~~~js
class Person {
	constructor(name, age) { // 这是类的构造器
		this.name = name;
		this.age = age;
	}
	say() {
		console.log(this.name, this.age);
	}
}

const p = new Person('Jack', 20);
p.say(); // Jack 20
~~~

每个类中都有一个构造器，如果我们手动指定构造器，那么默认类内部有个隐形的、看不见的空构造器，类似于`constructor() {}`

构造器的作用：`constructor`方法是类的默认方法，通过`new`命令生成对象实例时，自动调用该方法。一个类必须有`constructor`方法，如果没有显式定义，那么会默认添加一个空的`constructor`方法

也就是说，ES5 的构造函数Person，对应 ES6 的Person类的构造方法

~~~js
function Person {}

// 等同于
class Person {
  constructor() {}
}
~~~



**实例属性和静态属性**

**实例方法和静态方法**

通过`new`出来的实例能访问到的属性，叫做**实例属性**

通过构造函数，直接访问到的属性，叫做**静态属性**

ES5

~~~js
function Person(name, age) {
  this.name = name; // name是实例属性
  this.age = age; // age是实例属性
}

Person.msg = 'hello'; // msg是静态属性

Person.prototype.say = function() {
  console.log('这是Person的实例方法');
}

Person.show = function() {
	console.log('这是Person的静态方法');
}

const p = new Person('Jack', 18);

p.name; // Jack
p.age; // 18
p.say(); // 这是Person的实例方法
p.show(); // error, p.show is not a function
Person.show(); // 这是Person的静态方法
p.msg; // undefined
Person.msg; // hello
~~~

ES6

~~~js
class Person {
	constructor(name, age) { // 这是类的构造器
		this.name = name;
		this.age = age;
	}
	static msg = 'hello'; // 在class内部，通过static修饰的属性，就是静态属性

	say() { // 实例方法
		console.log('这是Person的实例方法');
  }

	static show() { // 静态方法
		console.log('这是Person的静态方法');
	}
}

const p = new Person('Jack', 20);
p.msg; // undefined
Person.msg; // hello
~~~



**类的继承**

在class中，使用extends关键字实现子类继承父类

父类

~~~js
class Person {
	constructor(name, age) {
		this.name = name;
		this.age = age;
	}
  say() {
   	console.log('大家好');
  }
}
~~~

子类

* 美国人

~~~js
class American extends Person {
	constructor(name, age) {
 		super(name, age); // 调用父类的constructor(name, age)
	}
}

let a = new American('Jack', 20 );
~~~

* 中国人(有身份证号独有)

~~~js
class Chinese extends Person {
	constructor(name, age, IDNumber) {
 		super(name, age); // 调用父类的constructor(name, age)
    this.IDNumber = IDNumber; // 语法规范：在子类中，this只能放到super之后使用
	}
}

let c = new Chinese('李三', 20, '450981******' );
~~~

1.为什么一定要在`constructor`中调用`super`?

答：因为如果一个子类通过extends关键字继承父类，那么在子类的constructor构造函数中必须优先调用super()

2.`super`是什么东西？

答： super是一个函数，他是父类的构造器，子类中的super其实就是父类中constructor构造器的一个引用

3.如果不调用`super`方法，子类就得不到 this 对象

~~~js
class Point {}

typeof Point; // function
Point === Point.prototype.constructor; // true
~~~

**class注意问题**

* 在class内部，只能写构造器，实例方法，静态属性，静态方法

~~~js
class Person {
	var a = 10; // 报错
}
~~~

* class关键字内部，还是用原来的ES5实现，我们把class关键字称作语法糖



