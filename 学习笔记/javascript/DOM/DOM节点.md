[TOC]



# DOM与节点

## 什么是DOM?

文档对象模型(Document Object Model)，又称为文档树模型。简单地说，DOM是一套对文档地内容进行抽象和概念化地方法。

**补充：**DOM是javascript的重要组成部分之一。是用来操作页面元素的一套API。

### DHTML

很多人可能会弄混淆DHTML其实是“Dynamic HTML”（动态HTML）的简称。DHTML并不是一项新技术，而是描述HTML、css和javascript技术组合的术语。



### DOM的组成

| **组成**   | **说明**                                   |
| :------- | :--------------------------------------- |
| 核心DOM    | 用于任何结构化文档和标准模型                           |
| XML DOM  | 用于XML文档的标准模型，定义了所有XML元素的对象和属性，以及访问它们的方法  |
| HTML DOM | 用于HMLT文档的标准模型，定义了所有HTML元素的对象和属性，以及访问它们的方法 |



---

## DOM节点

- 在HTML DOM中，所有事物都是节点。每一个节点都是一个对象

- 可以把DOM结构表示为一棵树。更具体地说，DOM把文档表示为一棵家谱树。parent(父)、child(子)、sibling(兄弟）等记号来表明家族成员之间的关系。
- HTML标签既没有父亲，也没有兄弟。如果这是一棵真正的树，<HTML>标签就是树根。


![节点树](E:\博客文档\DOM\节点树.jpg)







### DOM节点类型

- 整个文档都是一个文档节点
- 每个HTML元素是元素节点
- HTML内的文本是文本节点
- 每个HTML属性是属性节点
- 注释是注释节点


![节点类型](E:\博客文档\DOM\节点类型.jpg)





| 节点类型 | nodeName(只读) | nodeType（只读） | nodeValue     |
| ---- | ------------ | ------------ | ------------- |
| 元素   | 元素名称         | 1            | null          |
| 属性   | 属性名称         | 2            | 属性值           |
| 文本   | #text        | 3            | 文本内容（不包含HTML） |



**注意：**文本节点也可能是元素的子节点，如果想获取文本内容需要这样判断

```javascript
for (var i = 0; i < box.childNodes.length; i ++) {
	//判断是元素节点，输出元素标签名
	if (box.childNodes[i].nodeType === 1) {
		alert('元素节点：' + box.childNodes[i].nodeName);
	//判断是文本节点，输出文本内容
	} else if (box.childNodes[i].nodeType === 3) {
		alert('文本节点：' + box.childNodes[i].nodeValue);
	}
}
```

