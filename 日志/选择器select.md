### 选择符API

Selectors API(选择符API)是由W3C制定的一个标准，致力于让浏览器原生支持CSS查询。核心是两个方法：querySelector()和querySelectorAll() 支持IE8+。



### querySelector()方法

返回与该模式匹配的第一个元素。

```javascript
//取得body元素
var body = document.querySelector("body");

//取得ID为"myDiv"的元素
var myDiv = document.querySelector("#myDiv");

//取得类名为"selected"的第一个元素
var selected = document.querySelector(".selected");

```



### querySelectorAll()方法

方法接受的参数与querySelector()方法一样，通过CSS选择器获取元素，以**类数组**形式存在。可以传入复合选择器( 如：.box li, .box>li input[type='button'] )

```javascript
//取得某<div>中的所有<em>元素
var ems = document.getElementById('myDiv').querySelectorAll('em');

//取得类为"selected"的所有元素
var selecteds = document.querySelectorAll('.selected');

//取得所有<p>元素中的所有<strong>元素
var strongs = document.querySelectorAll('p strong');
```





