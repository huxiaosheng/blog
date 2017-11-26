# DOM #

- Document Object Model(文档对象模型)
- 可以把DOM结构表示为一棵树。更具体地说，DOM把文档表示为一棵家谱树。parent(父)、child(子)、sibling(兄弟）等记号来表明家族成员之间的关系。
- HTML标签既没有父亲，也没有兄弟。如果这是一棵真正的树，<HTML>标签就是树根。
- 每一个节点都是一个对象
- 节点分为不同的类型：元素节点、属性节点和文本节点


## 元素查找 ##
- **通过标签id查找元素节点：getElementByid(element);**
- **通过标签名查找元素节点：getELementsByTagName(element);**
- **通过类名查找元素节点：getElementsByClassName(element);**



## 属性节点的操作 ##



- **获取属性节点信息getAttribute(attribute)**
getAttribute()方法不属于document对象，所以不能通过document对象调用。它只能通过元素节点获取已经创建的属性

- **修改属性节点的值setAttribute(attribute,value)**
若在调用函数时atrribute属性不存在，函数会创建这个属性，然后设置它的值。
PS:不会更改静态文档里的源码内容

- **方法用于移除标签的属性removeAttribute(attribute)**




**nodeType属性**

每一个节点都有nodeType属性。

- 元素节点的nodeType属性值是1.
- 属性节点的nodeType属性值是2.
- 文本节点的nodeType属性值是3.


**nodeValue属性**

- 改变某个元素节点所包含的文本
- 改变文本，必须获取文本节点才可以用codevalue属性 





## 节点操作 ##

childNodes：获取所有子节点（包括元素节点和其他很多类型的节点）

children：获取所有子元素    (不是w3c标准，但是所有浏览器都支持)

nextSibling:下一个兄弟节点

nextElementSibing:下一个兄弟元素(IE678不兼容)

previousSibling:上一个兄弟节点

previousElementSibling:上一个兄弟元素(IE678不兼容)

firstChild:第一个子节点

firstElementChild:第一个子元素（IE678，不兼容）

lastChild:最后一个节点

lastElementChild:最后一个子元素（IE678不兼容）


parentNode:父节点  





BOM
window.open(ulr,name,features);