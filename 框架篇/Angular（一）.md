## Angular随笔一##

### Angular JS 是什么

​	Angular的官方文档是这样介绍它的。

> ​	完全使用javascript编写的客户端技术。同其他历史悠久的Web技术（HML、css、javascript）配合使用，使Web应用开发比以往更简单、更快捷。



它使web开发应用变得非常简单，同时也降低了构建复杂应用的难度。它提供了现代web应用中经常要用到的一系列高级功能，例如：

+ 解耦应用逻辑、数据模型和视图
+ Ajax服务
+ 依赖注入
+ 浏览历史
+ 测试



### AngularJs有什么不同

​	在其他javaScript框架中，我们被迫从自定义的javascriptjava script对象中进行扩展，并从外到内操作DOM。就以jQuery为例，为了在DOM中插入一个按钮元素，我们必须知道要把元素放到何处，并在合适的位置插入它：

```
var btn = $('<button>H1<button>');
btn.on('click',function(e){
  console.log("clicked button");
});
$('#checkout').append(btn);

```

​	尽管这个过程并不复杂，但是它要求开发者对整个DOM结构都有所了解，并强迫我们在JavaScript代码中加入复杂的控制逻辑，用以操作外部DOM。
​	而AngularJS则通过原生的Model-View-Controller（MVC，模型视图控制器）功能增强了HTML。结果表明，这个选择可以快捷和愉悦地构建出令人印象深刻并且极富表现力的客户端应用。
​	利用它，开发者可将页面的一部分封装为一个应用，并且不强迫整个页面都使用AngularJS进行开发。这个特质在某些情况下非常有用，比如你的工作流程中已经包含了另外一个框架，或者你只希望页面中的某一部分是动态的，而剩下的部分是静态的或者是由其他JavaScript框架来控制的。
​	此外，AngularJS团队非常重视框架文件压缩后的大小，这样使用它就不会付出太多的额外代价（写作本书时，文件压缩后的体积在90 KB左右）。这一特性使得AngularJS非常适合用于开发功能原型。



### 数据绑定

任何编程都使从hello world 开始 angular也不例外：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="angular.js"></script>
</head>
<body ng-app>

<input ng-model="name" type="text" placeholder="your name">
<h1>hello {{ name }}</h1>

</body>
</html>
```

  



## 四大核心特性

1. MVC
2. 模块化
3. 指令系统
4. 双向数据绑定

## mvc

MVC只是手段，终极目标是**模块化**和**复用**



**一切都是从模块开始的**









