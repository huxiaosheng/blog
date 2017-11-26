# Es6 新语法以及生疏的API

[TOC]



### 箭头函数

es6允许使用  `( => )` 定义函数

```javascript
var f = v => v;
```

等同于:

```javascript
var f = function(v){
	return v;
}
```





> () => {}

1. `()`等于定义 `function(){}` 匿名函数 
2. `{}` 为返回值



#### Example 1

```javascript
var f = () => 5   

>>>>>>

var f = function(){
	return 5;
}

```



#### Example 2

```javascript
var sun = (num1+num2) => {return num1+num2;}

>>>>
  
var sum = function(num1,num2){
	return num1+num2;
}

```



#### Example 3

```javascript
const full = ({first,last}) => first+' '+ last;

>>>>
  
  
const full = function(person){
  return person.first+' '+ person.last;
}
```





### Object.assign ()

方法只会拷贝源对象**自身的**并且**可枚举的**属性到目标对象身上。





### Array.prototype.slice()





### Array.prototype.fill()



### object.getOwnPropertyNames()

方法返回一个由指定对象的所有自身属性的属性名（包括不可枚举属性）组成的数组。



### object.keys()

> Object.keys(obj)

**obj**

​	返回枚举的属性的对象

**返回值**

​	返回给定对象的所有枚举属性的字符串数组



### Class扩展

js中生成实例对象的传统方法是通过构造函数,ES6提供了新的写法，引入了Class(类)这个概念作为对象的模版。通过`class`关键字，可以定义类。

基本上，ES6的`class`可以看作是一个语法糖,可以看以下例子ES5的写法。

```javascript
function Point(x,y){
  this.x = x;
  this.y = y;
}

Point.prototype.toString = function(){
  return '('+ this + ',' + this.y +')';
}

var p = new Point(1,2);
```



 ES6的写法:

```javascript
//定义类
class Point(){
  constructor(x,y){
    this.x = x;
    this.y = y;
  }
  
  toString(){
    return '('+ this + ',' + this.y +')';
  }
}
```



**ES6的类，完全可以看作构造函数的另一种写法**



**区别**

1. 类的内部所有定义的方法，都是不可枚举的(non-enumerable)
2. ES6不存在变量提升，不然报错。必须先定义后调用
3. 类必须用`new`调用否则报错。这是它跟普通构造函数的一个主要区别




### (...)扩展语句

**扩展语法**允许一个表达式在期望多个参数（用于函数调用）或多个元素（用于数组字面量）或多个变量（用于解构赋值）的位置扩展



我在react应用中看到了`{...this.props}`,意思就是接受父级传过来的所有属性







## Promise对象

异步编程的一种解决方案，



## Generator函数

### 基本概念

Generator函数是es6提供的一种异步编程解决方案。

直接上例子：

```javascript
function* helloWorldGenerator(){
    yield 'hello';
  	yield 'world';
  return 'ending';
}

var hw = helloWorldGenerator();
```

形式上，Generator函数是一个普通函数，但是有**两个特征**。

1. `function`关键字与函数名之间有一个星号
2. 函数体内部使用`yield`（产出）表达式，定义不同的内部状态







## async函数

一句话，就是Generator函数的语法糖



下面是一个Generator函数，依次读取两个文件。

```javascript
const fs = require('fs');

const readFile = function (fileName) {
  return new Promise(function (resolve, reject) {
    fs.readFile(fileName, function(error, data) {
      if (error) return reject(error);
      resolve(data);
    });
  });
};

const gen = function* () {
  const f1 = yield readFile('/etc/fstab');
  const f2 = yield readFile('/etc/shells');
  console.log(f1.toString());
  console.log(f2.toString());
};
```

写成`async`函数，就是这样

```Javascript
const asyncReadFile = async function(){
	const f1 = await readFile('/etc/fstab');
  	const f2 = await readFile('/etc/shells');
  	console.log(f1.toString());
  	console.log(f2.toStrong());
}
```

**特征：**Generator函数的星号(*)替换成`async`,将`yield`替换成`await`。