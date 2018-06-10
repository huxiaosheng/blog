# Es6 随笔

[TOC]



## let 和 const 

### let 命令

let 用于声明变量。类似于var .但是let有块级作用域 

```javascript
{
  let a = 10;
  var b = 20;
}

cosnole.log(a)  //not defined
console.log(b) 	//20;
```

**特点:**

1. **不存在变量提升**，及变量在声明语句之后才可以使用

2. **暂时性死区**，只要块级作用域内存在let命令，它所声明的变量就“绑定”这个区域，不再受外部影响

   ```javascript
   let tmp = 123;
   if(true){
       tmp = 'abc';
       console.log(tmp);
   }
   // abc
   let tmp = 123;
   
   if(true){   
       tmp = 'abc';
      	let tmp;
      	console.log(tmp);
   }
    //只要块级作用域内存在let命令，它所声明的变量就“绑定”这个区域，不再受外部影响,也不会去作用域外获取变量
    //ReferenceError
   ```


   ```



3. **不允许重复声明**，let不允许在想通作用域内重复声明同一个变量



### const命令

const声明一个只ou读的常量。一旦声明，常量的值就不能改变

**注意**

1. 作用域与let命令相同：只在声明所在的块级作用域内有效


### 块级作用域

es5只有全局作用域和函数作用域



## 字符串的拓展

### 模版字符串

   ```Javascript

name = 'imooc';
course='React 开发 App'

//老版
console.log('hello'+name+',course is '+course);

//新版
console.log(`hello${name},course is ${course}`);
   ```








## 变量的解构赋值

ES6允许按照一定模式从数组和对象中提取值，然后对变量进行赋值，这被称为解构(Destructuring)。

**注意**

1. 只要某种数据结构具有Iterator接口，都可以采用数组形式的解构赋值。

## 箭头函数

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





### 注意事项

1. 函数体内的this对象就是定义时所在的对象，而不是使用时所在的对象
2. 不可以当作构造函数。就是不可以使用new 命令，否则会抛出一个错误
3. 不可以使用arguments对象，该对象不存在。可以使用rest参数代替
4. 不可以使用yield命令，箭头函数不能用作Generator函数







## Set和Map数据结构

### SET

新的数据结构，**成员的值都是唯一的，没有重复**

- add(value)：添加某个值，返回Set结构本身
- delete(value)：删除某个值
- has(value)：
- clear()：



### Map

> javascript对象（Object）本质上是键值对的几个（hash结构），但是只能用字符串作为键。
>
> Map数据结构，“键”的范围不限于字符串，各种类型的值都可以当作键。



- Set(key,value)
- get(key)
- delete(key)

 



## Iterator和for...of

javascript表示“集合”的数据结构主要有数组（Array）和对象（Object），ES6又添加了Map和Set。







## Promise对象

异步编程的一种解决方案，



## Generator函数 

### 基本概念

Generator函数是es6提供的一种异步编程解决方案。

从语法上，可以把它理解成一个状态机，执行Generator函数会返回一个遍历对象。

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



### yiel表达式

Generator函数返回的遍历器对象只有调用next方法才会遍历下一个内部状态。所以其实提供了一种可以暂停的函数。yield语句就是暂停标志。











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



### async函数对generator函数的改进

1. async和await比



## Symbol

es6引入一种新的原始数据类型`Symbol`,表示独一无二的值。它是javascript语言的第7中数据类型。**只要属性名属于Symbol**类型，就是独一无二的，可以保证不会与其他属性名产生冲突





## **小tips**

### 关于结构的对象浅复制

es6有种新的赋值方式— 解构

> 按照一定模式从数组和对象中提取值，然后对变量进行赋值，这被称为解构 ( Destructuring )

```javascript
const obj = {a:1 ,b:2}
const obj2 = {...obj }	//{ a:1 ,b:2}
```

其实就是把obj所有的属性都复制到obj2里面，相当于对象的**浅复制**。如果要把一个对象的所有属性和值都赋值（深拷贝给一个对象的话），还可以覆盖，拓展对象属性如下：

```Javascript
const obj = { a:1,b:2}
const obj2 = {...obj, b:3 , c:4} // => { a: 1, b: 3, c: 4 }，覆盖了 b，新增了 c
```

### 什么是深拷贝和浅拷贝？

首先深拷贝和浅拷贝只正对像Object、Array 这样的复杂对象。简单来说，浅复制只是复制一层对象的属性，而深复制则递归复制了所有层级





### (...)扩展语句rest参数

**扩展语法**允许一个表达式在期望多个参数（用于函数调用）或多个元素（用于数组字面量）或多个变量（用于解构赋值）的位置扩展



我在react应用中看到了`{...this.props}`,意思就是接受父级传过来的所有属性



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





### object 语法片断



![es6_object](/Users/huyuan/Documents/Blog/images/es6_object.png)



### array 语法片断

![es6_array](/Users/huyuan/Documents/Blog/images/es6_array.png)