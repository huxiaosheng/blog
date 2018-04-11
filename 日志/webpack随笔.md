# webpack随笔

[TOC]



## 配置

```javascript
module.exports={
    target:'node/web'	//指定应该运行的环境
}
```









## plugins插件集合

### html-webpack-plugin

自动生成html文件的插件

```javascript
{	...,
    new HtmlWebpackPlugin({
        title:'标题'
    }),
    ...
}
```



### clean-webpack-plugin

主要在生成文件时删除之前的重复文件

```Javascript
{
    new CleanWebpackPlugin(['./dist'])
}
```





## situations

### 清除文件

#### 方法一:webpack插件（clean-webpack-plugin）

```javascript
//引入插件
const CleanWebpackPlugin = require('clean-webpack-plugin'); //使用前需要安装clean-webpack-plugin
new CleanWebpackPlugin(
     ['dist/main.*.js','dist/manifest.*.js'],　 //匹配删除的文件
     {
         root: __dirname,  //根目录
         verbose:  true,  //开启在控制台输出信息
         dry: false    //启用删除文件
     });
```



#### 方法二：node包 (rimarf)





## webpack-dev-server

webpack是一个小型的Node.js express服务器，webpack-dev-middleware 来服务webpack的包，除此之外还有一个Sock.js 来链接到服务器的微型运行时



- **webpack启动默认会从真实目录路中获取数据**
- **使用webpack-dev-server执行配置文件时，生成的包不会放在真实目录中，而是放在内存中**

### 版本兼容

- ^3.*  只兼容 webpack4.* 版本
- ^2.* 兼容webpack3.* 版本



### 报错 ：events.js 端口被占用

![屏幕快照 2018-04-06 上午2.11.10](/Users/huyuan/Documents/Blog/images/屏幕快照 2018-04-06 上午2.11.10.png)







## 模块热替换（HMR）

### webpack-dev-server和react-hot-loader的热加载区别 

**webpack-dev-server**:只能做到代码修改了页面也会自动刷新，开发人员修改了代码，代码经过打包，重新刷新了整个页面

**react-hot-loader**:不会刷新整个页面，它只替换了修改的代码，做到了页面的局部刷新。



### 坑

![屏幕快照 2018-04-08 下午11.56.06](/Users/huyuan/Documents/Blog/images/屏幕快照 2018-04-08 下午11.56.06.png)

一般在启用热更新的时候，如果使用这种方式渲染将会报错

```javascript
//hydrate 用于客户端和服务端混合渲染时使用
ReactDOM.hydrate(<App />, document.getElementById('root'))
```

**解决方法：**

```Javascript
const renderMethod = module.hot?ReactDOM.render : ReactDOM.hydrate
renderMethod(<App/>,document.getElementById('root'))
```

