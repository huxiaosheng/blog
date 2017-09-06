# webpack2 学习日志

[TOC]



## 什么是webpack

很多人可能觉得webpack是是个前端打包工具。其实不是，它是前端模块化的一个解决方案。

**核心思想**：一切都是模块

## 核心概念

- entry（入口）
- output（输出）
- loaders（加载器）
- plugins（插件）






## entry(入口)






## output（输出）

告诉webpack如何将编译好的文件写入磁盘。请注意，虽然可以有多个`entry`点，但只`output`指定了一个配置。





## babel

```javascript
{
  // babel 的核心功能模块，所有的 babel 包都依赖它
  "babel-core": "^6.24.0",
    
  // webpack 的 babel 加载器，带 JSX 编译支持
  "babel-loader": "^6.4.1",
    
  // ES2015语法支持，可以使用 ES6 最新特性
  "babel-preset-es2015": "^6.24.0",
    
  // 专为 react 优化，使代码支持 React ES6 classes 的写法，同时支持 JSX 语法格式
  "babel-preset-react": "^6.23.0",
      
}
```



















