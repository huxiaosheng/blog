# **React** 随笔    

[TOC]


## 核心

不是框架，只是一个库。它只提供UI(view)层面的解决方案。​

-  组件
-  JSX
-  Virtual DOM
>当组件状态 state 有更改的时候，React 会自动调用组件的 render 方法重新渲染整个组件的 UI。
>当然如果真的这样大面积的操作 DOM，性能会是一个很大的问题，所以 React 实现了一个Virtual DOM，组件 DOM 结构就是映射到这个 Virtual DOM 上，React 在这个 Virtual DOM 上实现了一个 diff 算法，当要重新渲染组件的时候，会通过 diff 寻找到要变更的 DOM 节点，再把这个修改更新到浏览器实际的 DOM 节点上，所以实际上不是真的渲染整个 DOM 树。这个 Virtual DOM 是一个纯粹的 JS 数据结构，所以性能会比原生 DOM 快很多。

- Data Flow




## JSX原理

**所谓的JSX其实就是javascript对象** ，是javascript语言的一种语法扩展，长的像HTML，但不是HTML。



**从jsx到页面的过程**：

![44B5EC06-EAEB-4BA2-B3DC-325703E4BA45](/Users/huyuan/Documents/Blog/images/44B5EC06-EAEB-4BA2-B3DC-325703E4BA45.png)

**总结**：

1. jsx 在编译的时候会变成相应的 javascript 对象描述
2. `react-dom` 负责把这个用来描述 UI 信息的 Javascript 对象变成DOM元素，并且渲染到页面上



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





### 组件的render方法

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

在jsx中可以传递任何`{}`包裹的javascript的代码，包括变量、表达式计算、函数执行等等。



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



## state VS props

### state 

主要作用于组件保存、控制、修改自己的可变状态。在组件内部初始化，可以被组件自生修改，而外部不能访问也不能访问也不能修改。你可以认为 `state` 是一个局部的、只能被组件自身控制的数据源。`state` 中状态可以通过 `this.setState`方法进行更新，`setState` 会导致组件的重新渲染。

### props

`props` 的主要作用是让使用该组件的父组件可以传入参数来配置该组件。它是外部传进来的配置参数，组件内部无法控制也无法修改。除非外部组件主动传入新的 `props`，否则组件的 `props` 永远保持不变。



### 总结：

`state` 和 `props` 有着千丝万缕的关系。它们都可以决定组件的行为和显示形态。一个组件的 `state` 中的数据可以通过 `props` 传给子组件，一个组件可以使用外部传入的 `props` 来初始化自己的 `state`。但是它们的职责其实非常明晰分明：*state 是让组件控制自己的状态，props 是让外部对组件自己进行配置*。

没有 `state` 的组件叫无状态组件（stateless component），设置了 state 的叫做有状态组件（stateful component）。因为状态会带来管理的复杂性，我们尽量多地写无状态组件，尽量少地写有状态的组件。这样会降低代码维护的难度，也会在一定程度上增强组件的可复用性。前端应用状态管理是一个复杂的问题，我们后续会继续讨论。





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





## props.children和容器类组件



## 受控组件和非受控组件

### 受控组件

当用户提交表单时，HTML的默认行为会使这个表单跳转到一个新页面。在React中亦是如此。但是大多数情况下，**我们都会构造一个处理提交表单并可访问用户输入表单数据的函数。实现这一点的标准方法是使用一种称为“受控组件”的技术**

简单点说：**其值由React控制的输入表单元素称为“受控组件”**



### 非受控组件

在大多数情况下，我们推荐使用`受控组件`来实现表单。受控组件中，表单数据由React组件处理。如果让表单数据由DOM处理时，代替方案为使用**非受控组件**





## 高阶组件

就是一个函数，传给它一个组件，它返回一个新的组件

**作用**：为了组件之间的代码复用，组件可能有着某些相同的逻辑，把这些逻辑抽离出来，放到高阶组件中进行复用。高阶组件内部的包装组件和被包装组件之间通过props传递数据

**注意**：关于组件执行顺序的事

1. 父组件与子组件，父组件先执行，子组件后执行
2. 普通组件和高阶组件，高阶组件先执行，被包装组件后执行

![高阶组件 2018-03-11 上午3.17.36](/Users/huyuan/Documents/Blog/images/高阶组件 2018-03-11 上午3.17.36.png)

上面的代码是一个多层高阶组件的调用，正常的思维会认为先执行`wrapWithAjaxData`，再执行`wrapWithLoadData`,其实相反，前面的两个语句是赋值语句，并没用真正的调用函数。调用函数的操作其实是在父组件调用这个`CommentInput`组件时才会调用这个函数的。所以这么看的话,就是`wrapWithAjaxData` 外面包着`wrapWithLoadData`，然后调用的时候会先调用外面一层的高阶组件。

wrapWithLoadData—>wrapWithAjaxData—>CommentInput





## Immutable.js 是什么？

Immutable.js 是一个完全独立的库，无论基于什么框架都可以用它。

- 意义在于它弥补了javascript 没有不可变数据结构的问题。不可变数据结构是函数式编程中必备的。
- 在React开发中，频繁操作state对象或是store，配合immutableJs快、安全



## `react`的虚拟DOM

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







## react 的事件监听

例子：

```Jsx
render(){
  return (
  	<h1 onClick="this.handleClickOnTitle">React 小书</h1>
  )
}
```





1. 在React.js不需要手动调用浏览器原生的`addEventListener`进行事件监听。React .js 帮我们封装好了一些列的`on*`属性，当你需要为某个元素监听某个事件的时候，只需要简单的给它加上`on*`就可以了.
2. 没有经过特殊处理的话，**`on*`事件监听只能用在普通的HTLML的标签上，而不能用在组件标签上。**
3. 和普通浏览器一样，事件监听函数会被自动传入一个 `event` 对象，这个对象和普通的浏览器 `event` 对象所包含的方法和属性都基本一致。不同的是 React.js 中的 `event` 对象并不是浏览器提供的，而是它自己内部所构建的。



## 状态提升的弊端

​	**状态提升**：当某个状态被多个组件*依赖*或者*影响*的时候，就把该状态提升到这些组件的最近公共父组件中去管理，用 `props` 传递*数据或者函数*来管理这种*依赖*或着*影响*的行为。

​	但是如果这个状态，需要被更高的组件用。你就得继续提升。你会发现这种无限制的提升不是一个好的解决方案。一旦发生了提升，你就需要修改原来保存这个状态的组件的代码，也要把整个数据传递路径经过的组件都修改一遍。所以我们需要一个方案，**Redux** 就是状态管理工具来帮助我们来管理这种共享状态。







## React.js 的 context 

react组件树中的状态想要传递，需要一级一级通过`props`传递。这样很麻烦，但是还有一种共享状态的API，`context`相当于js的window，其实就是组件树上某颗子树的全局变量

用法:



```Javascript

class Index extends Component{
  //功能和	propTypes验证组件props参数作用类似，不过它验证的是getChildContext返回的对象
  static childContextTypes = {
    themeColor:PropTypes.string
  }

  constructor(){
    super()
    this.state = {themeColor:'red'}
  }


//设置context的过程，它返回对象就是context
  getChildContext(){
    return {themeColor:this.state.themeColor}
  }


  render(){
    return...
  }
}

class Title extends Component{
  //获取context共享的值
  static contextTypes = {
    themeColor:PropTypes.string
  }



  render(){
    return (this.context.themeColor)
  }
}
```









## 纯函数（Pure Function）

纯函数，是**函数式编程**里面非常重要的概念。简单来说，**一个函数的返回结果只依赖于它的参数，并且执行过程里面没有副作用，我们就把这个函数叫做纯函数**。

#### 什么是副作用？

在函数执行过程中对外部的数据产生了影响，就是副作用。

#### 纯函数的好处

1. 大量使用函数，减少代码的重复，提高开发速度
2. 函数式编程不依赖、也不会改变外界的状态，方便代码的维护和管理







## 组件的生命周期

**挂载**：我们把React.js将组件渲染，并且构造DOM元素然后塞入页面的过程称为组件的挂载。

### 挂载阶段

- componentWillMount : 组件挂载开始之前，也就是在组件调用`render`方法之前调用
- componentDidMount : 组件挂载完成之后，也就是DOM元素已经插入页面后调用
- componentWillUnmount : 组件对应的DOM元素从页面中删除之前调用



```
--> constructor()
--> componentWillMount()   //组件挂载之前
--> render()
//然后构造DOM元素插入页面（挂载）
--> componentDidMount()    //组件挂载完成之后
//...
--> componentWillUnmount()
// 从页面中删除
```





### 更新阶段

- shouldComponentUpdate(nextProps,nextState) : 你可以通过这个方法控制组件是否重新渲染。如果返回`false`组件就不会重新渲染。这个生命周期在React.js性能优化上非常有用。

- componentWillReceiveProps(nextProps) ：组件从父组件接受到新的`props`之前调用

- componentWillUpdate() : 组件开始重新渲染之前调用

- componentDidUpdate() : 组件重新渲染并且把更改变更到真实的DOM以后调用

  ​





##  PropTypes

提供一系列的数据类型可以用来配置组件的参数

```
PropTypes.array
PropTypes.bool
PropTypes.func
PropTypes.number
PropTypes.object
PropTypes.string
PropTypes.node
PropTypes.element

```





## 开发规范

- 组件的私有方法都用`_`开头，所有事件监听的方法都用`handle`开头。
- 把事件监听方法传给组件的时候，属性名用`on`开头。





内容编写循序如下 :

```
1. static 开头的类型属性，如 defaultProps、propTypes
2. 构造函数，constructor
3. getter/setter 
4. 组件生命周期
5. _开头的私有方法
6. 事件监听方法，hanle*.
7. render* 开头的方法，有时候render() 方法里面的内容会分开到不同函数里面进行，这些函数都以 render* 开头
```





### 目录结构

- 按角色组织
- 按功能组织

