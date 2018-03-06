# Redux 随笔

### 什么是Redux？

一种新型的前端“架构模式”，和React-redux并不是同一个东西。Redux是Flux 架构的一种变种。





### Redux源码的设计思路



```javascript



function stateChanger(state, action) {
  
    if (!state) {
        return {
            title: {
                text: 'React.js小书',
                color: 'red',
            },
            content: {
                text: 'React.js 小书内容',
                color: 'blue'
            }
        }
    }

    switch (action.type) {
        case 'UPDATE_TITLE_TEXT':
            return {
                ...state,
                title: {
                    ...state.title,
                    text: action.text
                }
            }
        case 'UPDATE_TITLE_COLOR':
            return {
                ...state,
                title: {
                    ...state.title,
                    color: action.color
                }
            }
        default:
            return state 
    }

}


function renderApp(newAppState, oldAppState = {}) {
    if (newAppState === oldAppState) return
    renderTitle(newAppState.title, oldAppState.title)
    renderContent(newAppState.content, oldAppState.content)
}


function renderTitle(newTitle, oldTitle = {}) {
    if (newTitle === oldTitle) return
    const titleDOM = document.getElementById('title')
    titleDOM.innerHTML = newTitle.text
    titleDOM.style.color = newTitle.color
}

function renderContent(newContent, oldContent = {}) {
    if (newContent === oldContent) return
    const contentDOM = document.getElementById('content')
    contentDOM.innerHTML = newContent.text
    contentDOM.style.color = newContent.color
}



//1.Redux 的核心代码
//参数：reducer 是一个纯函数。用来定义修改状态的规则
//返回值：
//getState:获取当前状态
//dispatch：通过传入的action，执行reducer去修改状态
//subscribe:主要用来监听数据变化的，每次对store 进行dispatch(action)都会触发subscribe注册的函数调用。主要看自己的应用场景。来编写不同的函数。添加到subscribe中

function createStore(reducer) {
    let state = null
    const listeners = []
    const subscribe = (listener) => listeners.push(listener)
    const getState = () => state
    const dispatch = (action) => {
        state = reducer(state, action)
        listeners.forEach((listener) => listener())
    }
    dispatch({})
    return { getState, dispatch, subscribe }
}

const store = createStore(stateChanger)
let oldState = store.getState()//缓存旧的state



store.subscribe(() => {
    const newState = store.getState()   //数据可能变化，获取新的state
    renderApp(newState, oldState)
    oldState = newState

})

renderApp(store.getState())//首次渲染页面
store.dispatch({ type: 'UPDATE_TITLE_TEXT', text: '《React.js小书》' })    
store.dispatch({ type: 'UPDATE_TITLE_COLOR', color: 'blue' })
// renderApp(appState) //把新的数据渲染到页面上


```





#### 1. 模块（组件）之间需要共享数据，这些模块（组件）还可能需要修改这些共享数据

**矛盾**：“模块之间需要共享数据”，和“数据可能被任意修改导致不可预料的结果”之间的矛盾。

**解决方法：** *提高数据修改的门槛*，组件之间可以共享数据，也可以改数据。但是数据不能直接改，你只能执行某些我允许的某些修改。

所有对数据的操作必须通过 `dispath` 函数。它接受一个参数 `action` ，这个 `action` 是普通的 javascript 对象，里面必须包含一个 type 字段来声明你到底想干什么。

```Javascript
function dispatch(action){
  switch (action.type){
    case 'UPDATE_TITLE_TEXT':
      appState.title.text = action.text
      break
    case 'UPDATE_TITLE_COLOR':
      appState.title.color= action.color
      break
    default:
      break
  }
}
```





所以提高了修改数据的门槛：你必须通过 `dispatch` 执行某些允许的修改操作，而且必须大张旗鼓的在 `action`里面声明。

然后我们把它抽象出来一个`createStroe`,它可以产生`store`，里面包含`getState`和`dispath`函数，方便我们使用。



#### 2. 后来发现每次修改数据都需要手动重新渲染非常麻烦，我们希望自动重新渲染视图。



#### 3. 重新渲染有严重的性能问题，我们引用了“共享结构的对象”来帮我们解决问题

```javascript
//定一个reducer
function reducer(state,action){
  /* 初始化 state 和 switch case */
}

//生成store
const store = createStore(renducer)

//首次渲染页面
renderApp(store.getState())

//后面可以随意dispatch了，页面自动更新
store.dispatch(...)



```





## React-redux实现

关于React 的应用状态管理中提过，前端中应用的状态存在的问题：就是**状态提升**，一个状态可能被组件树上的所有关联的组件依赖或者影响，并且如果一直有更高级的组件应用，就必要不断的提升状态。而React.js 并没有提供好的解决方案，我们只能把状态提升到依赖或者影响这个状态的所有组件的公共组件上，我们把这种行为叫做状态提升。但是需求不停变化，共享状态没完没了的提升，不符合前端的耦合、可复用、可维护。

### React-redux

其实就是结合content和Store，通过content 共享状态，store.dispatch 修改状态。























