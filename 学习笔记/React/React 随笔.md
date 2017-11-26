# React 随笔    

## 核心

-  组件
-  JSX
-  Virtual DOM
>当组件状态 state 有更改的时候，React 会自动调用组件的 render 方法重新渲染整个组件的 UI。
>当然如果真的这样大面积的操作 DOM，性能会是一个很大的问题，所以 React 实现了一个Virtual DOM，组件 DOM 结构就是映射到这个 Virtual DOM 上，React 在这个 Virtual DOM 上实现了一个 diff 算法，当要重新渲染组件的时候，会通过 diff 寻找到要变更的 DOM 节点，再把这个修改更新到浏览器实际的 DOM 节点上，所以实际上不是真的渲染整个 DOM 树。这个 Virtual DOM 是一个纯粹的 JS 数据结构，所以性能会比原生 DOM 快很多。

- Data Flow


### JSX
```javascript
ReactDOM.render(
          <h1>Hello, world!</h1>,
          document.getElementById('example')
        );
        
```
HTML 语言直接写在 JavaScript 语言之中，不加任何引号，这就是 JSX 的语法，它允许 HTML 与 JavaScript 的混写。

**在JSX里写js用大括号套住就可以了**

### state
React 把组件看成是一个状态机（State Machines）。通过与用户的交互，实现不同状态，然后渲染 UI，让用户界面和数据保持一致。

React 里，只需更新组件的 state，然后根据新的 state 重新渲染用户界面（不要操作 DOM）

  1. **getInitialState** 方法用于定义初始状态，也就是一个对象，这个对象可以通过
  2. **this.state** 属性读取。当用户点击组件，导致状态变化，
  3. **this.setState** 方法就修改状态值，每次修改以后，自动调用 this.render 方法，再次渲染组件。



### props
state 和 props 主要的区别在于 props 是不可变的，而 state 可以根据与用户交互来改变。这就是为什么有些容器组件需要定义 state 来更新和修改数据。 而子组件只能通过 props 来传递数据。

**props只能通过父组件传给子组件**







## 组件周期

