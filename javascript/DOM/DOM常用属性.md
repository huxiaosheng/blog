[TOC]



## 获取元素

### 方法一

| 方法                       | 说明                |
| ------------------------ | ----------------- |
| getElementById()         | 通过id获取元素节点        |
| getElementsByTagName()   | 通过标签名获取节点（返回数组）   |
| getElementsByClassName() | 通过class获取节点（返回数组） |

**getElementsByClassName() 建议不要使用IE678不支持，有兼容问题**



### 方法二

`querySelector()`和`querySelectorAll()`

```javascript
// 通过querySelector获取ID为q1的节点：
var q1 = document.querySelector('#q1');

// 通过querySelectorAll获取q1节点内的符合条件的所有节点：
var ps = q1.querySelectorAll('div.highlighted > p');
```



**注意：**

严格地讲，我们这里的DOM节点是指`Element`(元素)，但是DOM节点实际上是`Node`，在HTML中，`Node`包括`Element`、`Comment`、`CDATA_SECTION`等很多种，以及根节点`Document`类型，但是，绝大多数时候我们只关心`Element`，也就是实际控制页面结构的`Node`，其他类型的`Node`忽略即可。根节点`Document`已经自动绑定为全局变量`document`。



## 操作元素属性

 ### 点方式

```javascript
console.log(ele.value)  //获取元素中value属性的值
ele.value = "aaa"  		//设置标签中value属性的值

ele.disabled = true;	//该文本框本被禁用

ele.className = 'aaa'	//设置元素class 属性
```



### 自定义属性

| 方法                | 说明        |
| ----------------- | --------- |
| getAttribute()    | 获取元素节点属性的 |
| setAttribute()    | 设置元素节点的属性 |
| removeAttribute() | 移除元素节点属性  |



### 节点的层次

| 节点方法            | 说明                     |
| --------------- | ---------------------- |
| childNodes      | 获取所有子节点（不包括元素节点和其他类型的） |
| firstChild      | 获取第一个子节点               |
| lastChild       | 获取最后一个子节点              |
| nextSibling     | 获取下一个兄弟节点              |
| previousSibling | 获取上一个兄弟节点              |
| parentNode      | 获取父节点                  |

###### ![节点层次](E:\博客文档\DOM\节点层次.jpg)

**注意：上面的节点层次图，是指所有的节点，如文本节点也可以是Node**



| 元素层次方法                 | 说明        |
| ---------------------- | --------- |
| children  ( 无兼容问题 )    | 获取所有子元素   |
| firstElementChild      | 获取第一个子元素  |
| lastElementChild       | 获取最后一个子元素 |
| nextElementSibing      | 获取下一个兄弟元素 |
| previousElementSibling | 获取上一个兄弟   |

**PS:上面的表格中的方法是直接获取元素节点的。存在IE678的兼容问题**







