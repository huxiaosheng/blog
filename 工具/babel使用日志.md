# babel+webpack 配置

因为目前babel通常会和webpack 结合一起去使用，所以就以webpack为例



### 配置文件.babelrc

Babel 的配置文件是.babelrc，存放在项目的根目录下。使用Babel的第一步就是配置这个文件

**安装**

````
npm i  babel-preset-env -D
````

这个用来设置转码规则和插件

```
{
    "presets":["env"],
    "plugins":[]
}
```

**如果要使用React,支持jsx语法 **

```
//安装
npm i babel-preset-react -D
```

```
//babelrc
{

    "presets":["env","react"],
    "plugins":[]
}

```



### 使用webpack

```
//安装
npm i babel-loader babel-core
```

**babel-loader**: webpack处理新语法的加载器

**babel-core**:如果某些代码需要调用BabeldeAPi进行转码，就要使用babel-core模块。

```
//webpack的配置
module: {
  rules: [
    { test: /\.js$/, exclude: /node_modules/, loader: "babel-loader" }
  ]
}
```





### 

