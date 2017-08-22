# Es6 新语法以及生疏的API

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





