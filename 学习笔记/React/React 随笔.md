# React 随笔    

[TOC]


## 核心

-  组件
-  JSX
-  Virtual DOM
>当组件状态 state 有更改的时候，React 会自动调用组件的 render 方法重新渲染整个组件的 UI。
>当然如果真的这样大面积的操作 DOM，性能会是一个很大的问题，所以 React 实现了一个Virtual DOM，组件 DOM 结构就是映射到这个 Virtual DOM 上，React 在这个 Virtual DOM 上实现了一个 diff 算法，当要重新渲染组件的时候，会通过 diff 寻找到要变更的 DOM 节点，再把这个修改更新到浏览器实际的 DOM 节点上，所以实际上不是真的渲染整个 DOM 树。这个 Virtual DOM 是一个纯粹的 JS 数据结构，所以性能会比原生 DOM 快很多。

- Data Flow




## JSX语法

本质上来讲，jsx只是为了`React.createElement(component,props,...children)`方法提供的语法糖。比如：

```html
<MyButton color="blue" shadowSize={2}>
  Click me
</MyButton>
```

编译为：

```jsx
React.createElement(
  MyButton,
  {color:'blue',shadowSize:2},
  'Click me'
)
```


### 注意

#### React必须声明

由于jsx编译后会调用React.createElement方法，所以在你的jsx代码中必须先申明React变量



#### 点表示法

jsx中可以点表示法来引用React组件。你可以方便地从一个模块中导出许多React组件。

```Jsx
import React from 'react';

const MyComponents = {
  DatePicker:function DatePicker(props){
    return <div>Imagine a {props.color} datepicker here.</div>;
  }
}

function BlueDatePicker(){
  return <MyComponents.DatePicker color="blue" />;
}
```



### 使用javascript表达式

在jsx中可以传递任何`{}`包裹的javascript表达式作为一个属性值。



## 组件

### React.createClass

用于生成一个组件类

```javascript
var HelloMessage = React.createClass({
  render:function(){
    return <h1>Hello {this.props.name}</h1>;
  }
});

ReactDOM.render(
	<HelloMessage name="Runoob"/>,
  	document.getElementById('example')
)
```



## state
React 把组件看成是一个状态机（State Machines）。通过与用户的交互，实现不同状态，然后渲染 UI，让用户界面和数据保持一致。

React 里，只需更新组件的 state，然后根据新的 state 重新渲染用户界面（不要操作 DOM）

    1. **getInitialState** 方法用于定义初始状态，也就是一个对象，这个对象可以通过
    2. **this.state** 属性读取。当用户点击组件，导致状态变化，
    3. **this.setState** 方法就修改状态值，每次修改以后，自动调用 this.render 方法，再次渲染组件。



## props
- state 和 props 主要的区别在于 props 是不可变的，而 state 可以根据与用户交互来改变。
- 这就是为什么有些容器组件需要定义 state 来更新和修改数据。 
- 而子组件只能通过 props 来传递数据。

**props只能通过父组件传给子组件**

```
getDefaultProps()：方法为props设置默认值
```





## 组件API

- 设置状态 : setState
- 替换状态：replaceState
- 设置属性：setProps
- 替换属性：replaceProps
- 强制更新：forceUpdate
- 获取DOM获取节点：findDOMNode
- 判断组件挂载状态：isMounted






## 状态提升

在React中，状体分享是通过将state数据提升至离需要这些数据的组件最近的父组件来完成的。这就是所谓的**状态提升**，

状态提升比双向绑定方式要写跟多的“模版代码”，但带来的好处是，你也可以更快地寻找和定位bug的工作。因为哪个组件保有状态数据，也只有它自己能够操这些数据，发生bug的范围就被大大地减小了。此外，你也可以使用自定义逻辑来拒绝活着更改用户的输入



## state和props重要区别

**props**：是一种从父级向子级传递数据的方法。

**state**：只在交互的时候使用，即随时间变化的数据。

所以在构建一个用于呈现数据模型的静态版本的应用程序，你只需要创建能够服用其他组件的组件，并通过props来传递数据。



## Refs & DOM

我们都知道在典型的React数据流中，props是父组件与子代交互的唯一的方式。

但是，在某些情况下你需要在典型数据流外强制修改子代。要修改的子代可以是React组件实例，也可以是DOM元素。

### 何时使用Refs

- 处理焦点、文本选择或媒体控制
- 触发强制动画。
- 集成第三方DOM库



**React支持给任意组件添加特殊属性。`ref`属性接受一个回调函数，它在组件被加载或卸载时会立即执行**



#### 为DOM元素添加Ref

当给`html`元素添加`ref`属性时，`ref`回调接收了底层的DOM元素作为参数。

```jsx
class CustomTextInput extends React.Component{
  constructor(props){
    super(props);
    this.focus = this.focus.bind(this);
  }
  
  focus(){
    //直接使用原生API focus()使text输入框获得焦点
    this.textInput.focus();
  }
  
  render(){
    //使用`ref`的回调将text输入框DOM节点，存储到React this.textInput变量中
    //参数input是DOM节点
    return (
    <div>
    <input type="text" ref={(input)=>{this.textInput = input}}/>  
      </div>
    )
  }
}
```





## 受控组件和非受控组件

### **受控组件**

当用户提交表单时，HTML的默认行为会使这个表单跳转到一个新页面。在React中亦是如此。但是大多数情况下，**我们都会构造一个处理提交表单并可访问用户输入表单数据的函数。实现这一点的标准方法是使用一种称为“受控组件”的技术**

简单点说：**其值由React控制的输入表单元素称为“受控组件”**



### 非受控组件

在大多数情况下，我们推荐使用`受控组件`来实现表单。受控组件中，表单数据由React组件处理。如果让表单数据由DOM处理时，代替方案为使用**非受控组件**





## react的虚拟DOM

React在渲染出的UI内部建立和维护了一个内层的实现方式，它包括了从组件返回的React元素。这种实现方式使得React避免了一些不必要的创建和关联DOM节点，因为这样做可能比直接操作JavaScript对象更慢一些。有时它被称之为“虚拟DOM”，但是它其实和React Native的工作方式是一样的

当一个组件的`props`或者`state`改变时，React通过比较新返回的元素和之前渲染的元素来决定是否有必要更新实际的DOM。当他们不相等时，React会更新DOM。

在一些情况下，你的组件可以通过重写这个生命周期函数`shouldComponentUpdate`来提升速度， 它是在重新渲染过程开始前触发的。 这个函数默认返回`true`，可使React执行更新：



如果你知道在某些情况下你的组件不需 要更新，你可以在`shouldComponentUpdate`内返回`false`来跳过整个渲染进程，该进程包括了对该组件和之后的内容调用`render()`指令。





## React 启发O(n)算法

1. 两个不同类型的元素将产生不同的树
2. 通过渲染器附带`key`属性，开发者可以示意可能是稳定的

实践中，上述假设适用于大部分应用场景

## React的生态圈

1. 路由

   React-router

2. 状态管理器

   Redux、mobx目前最受欢迎的两个

   Mobx 适合做一些简单的应用，原型实验，适合小的团队使用。Mobx 的优点是响应状态的变化。

   redux适合复杂的应用，大团队，需求变化多。它的优点是响应动作和事件。
   redux不仅应用于react，也可以应用于angular，vue等框架，只是redux和react配合使用最为契合。

   另外国内蚂蚁金服前端团队基于redux, react-router打造了另一个前端框架——[dva](https://link.zhihu.com/?target=https%3A//github.com/dvajs/dva)。
   [dva](https://link.zhihu.com/?target=https%3A//github.com/dvajs/dva)简单来讲是对redux方案的集成与拓展，它突破框架的本身，形成一套略为完整的前端架构，处理了很多包括项目构建，异步处理、统一请求、统一错误处理等一系列诸多问题。

3. UI库

   首先国外的有[material-ui](https://link.zhihu.com/?target=https%3A//github.com/callemall/material-ui)、[react-toolbox](https://link.zhihu.com/?target=http%3A//react-toolbox.com/)。它们都基于谷歌的[material](https://link.zhihu.com/?target=https%3A//material.io/guidelines/)设计理念，因此界面非常精美，尤其适用于web开发。

   其次是国内蚂蚁金服开源的[ant design](https://link.zhihu.com/?target=https%3A//ant.design/index-cn)，以及百分点公司开源的[bfd-ui](https://link.zhihu.com/?target=http%3A//ui.baifendian.com/)。这两个都是企业级的UI库，提供的组件极其丰富，此外逻辑交互也处理得非常好，基本不需要你操作过多的业务逻辑即可完成开发。

   ​

   ​



