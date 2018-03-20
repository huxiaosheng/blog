# Koa

[TOC]

​	基于Node.js平台的下一代web开发框架。通过组合不同的generator,可以避免重复繁琐的回调函数嵌套，避免重复繁琐的回调函数嵌套。

**Ps** :generator是es6提供的一种异步编程解决方案



## Koa-route(路由)

```
const route = require('koa-route');

const about = ctx => {
  ctx.response.type = 'html';
  ctx.response.body = '<a href="/">Index Page</a>';
};

const main = ctx => {
  ctx.response.body = 'Hello World';
};

app.use(route.get('/', main));
app.use(route.get('/about', about));
```



## koa-static

可以获取静态资源



## koa-compse

可以将多个中间件合成为一个



## 中间件(middleware)

基本上，Koa所有的功能都是通过中间件实现的。那么什么是中间件呢？

> 处在HTTP Request 和 HTTP Response 中间，用来实现某种中间功能。app.use()用来加载中间件。
>
> 每个中间件默认接受两个参数，第一个参数是**Context**对象，第二个参数是**next**函数。只要调用**next** 函数，就可以把执行权交给下一个中间件。

**注意**：每个中间件必须通过app.use()调用。



## 中间件栈

多个中间件会形成一个站结构(middle stack),以”先进后出“(first-in-last-out)的顺序执行。

```
1.最外层的中间件首先执行。
2.调用next函数，把执行权交给下一个中间件。
3....
4.最内层的中间件最后执行。
5.执行结束后，把执行权交回上一层的中间件。
6....
7.最外层的中间件收回执行权之后，执行next函数后面的代码。
```



Example

```
const one = (ctx, next) => {
  console.log('>> one');
  next();
  console.log('<< one');
}

const two = (ctx, next) => {
  console.log('>> two');
  next(); 
  console.log('<< two');
}

const three = (ctx, next) => {
  console.log('>> three');
  next();
  console.log('<< three');
}

app.use(one);
app.use(two);
app.use(three);


>>>>>>>>结果>>>>>>>>>>>>>

>> one
>> two
>> three
<< three
<< two
<< one

```





## 错误处理



`ctx.throw()`方法，用来抛出错误,`ctx.throw(500)`就是抛出500错误





## 常用中间件

### koa-bodyparser

koa的`body`分析器,基于`co-body`

#### 基本用法

```Javascript
var Koa = require('koa');
var bodyParser = require('koa-bodyparser');

var app = new Koa();
app.use(bodyParser());

app.use(async ctx=>{
  //解析的机构将被存在`ctx.request.body`
  ctx.body = ctx.request.body;
  
})
```

