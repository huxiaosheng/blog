# npm随笔

[TOC]



### nrm NPM的镜像管理工具

```javascript
npm install -g nrm //安装nrm包

nrm ls	//列出可选的源

nrm use taobao //切换taobao源

```



### 常用快捷键

```javascript
i	表示	install		//下载
-g	表示	--global	//全局
-S	表示	--save		//生产环境依赖
-D	表示	--save-dev	//开发环境依赖
```

#### package初始化

> ​	npm init -f



### 下载包版本

> 遵循“大版本.次要版本.小版本”的格式规定

`npm  i jquery@1.2.2`

- 指定版本：比如1.2.2，遵循“大版本.次要版本.小版本”的格式规定，安装时只安装指定版本。


- 波浪号+指定版本：比如~1.2.2，表示安装1.2.x的最新版本（不低于1.2.2），但是不安装1.3.x，也就是说安装时不改变大版本号和次要版本号。


- 插入号+指定版本：比如ˆ1.2.2，表示安装1.x.x的最新版本（不低于1.2.2），但是不安装2.x.x，也就是说安装时不改变大版本号。需要注意的是，如果大版本号为0，则插入号的行为与波浪号相同，这是因为此时处于开发阶段，即使是次要版本号变动，也可能带来程序的不兼容。

`latest：安装最新版本。`





## 包



### 设置跨平台环境变量**cross-env** 

当你`NODE_ENV=production`设置环境变量时，在不同的系统运行的结果可能是不一样的，所有就有一个包实现快环境设置环境变量

```Javascript
{
    script:{
        "build":"cross-env NODE_ENV = production webpack --config build/webpack.config.js"
    }
}
```



