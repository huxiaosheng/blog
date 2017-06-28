# node 学习 ---廖雪峰（一）

[TOC]

## 模块

在Node环境中，一个`.js`文件就称之为一个模块(module)。



**总结** 

要在模块中对外输出变量，用:

> module.exports = variable;

输出的变量可以是任意对象、函数、数组等等。

要引入其他模块输出的对象，用：

> var foo = require('other_module');

引入的对象具体是什么，取决于引入模块输出的对象。`other_module`为绝对路径。



### module.exports vs exports

在Node环境中，有两种方法可以在一个模块中输出变量：

**方法一：对module.exports赋值**

```javascript
//hello hs

function hello(){
  console.log("hello, world");
}

function greet(){
  console.log('hello,' + name + '!');
}

module.exports = {
  hello:hello,
  greet:greet
}
```



**方法二：直接使用exports**

```javascript
//hello.js
function hello(){
	console.log('hello,world');
}

function greet(name){
  console.log('hello'+ name + '!');
}}

exports.hello = hello;
exports.greet = greet;
```

但是你不可以直接对`exports`赋值：

```
exports = {
 	hello:hello,
    greet:greet
}
```



**结论**

1. 如果要输出一个键值对象{},可以利用`exports`这个已存在的空对象{}；并继续在上面添加新的键值；
2. 如果要输出一个函数过数组，必须直接对`module.exports`对象赋值
3. 所以我们可以得出结论：直接对`module.exports`赋值，可以应对任何情况。

