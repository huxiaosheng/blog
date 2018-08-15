# React 动画

react中动画的实现方式大致分以下几种：

1. 基于定时器或RAF的间隔动画
2. 基于css3 的简单动画
3. react动画API `CssTransitionGroup`
4. 第三方动画库

## 一、基于定时器或RAF的间隔动画

最早的动画都是依靠定时器`setInterval`、`setTimeout`直接通过修改DOM元素的属性。还有html5提供的专门用于请求动画的API，即**requestAnimationFrame(rAF)**,顾名思义就是“请求帧动画”。

### 动画原理

我们电脑屏幕一般刷新频率为60HZ，由于频率很高，**当你对着电脑屏幕什么也不做的情况下，显示器也会以每秒60次的频率正在不断的更新屏幕上的图像**。而 **动画本质就是要让人眼看到图像被绘制而引起变化的视觉效果，这个变化要以连贯的、平滑的方式进行过渡。** 

### setTimeout的缺点

- setTimeout 的执行时间并不是确定的。在JavaScript中， setTimeout 任务被放进了异步队列中，只有当主线程上的任务执行完以后，才会去检查该队列里的任务是否需要开始执行，所以 **setTimeout 的实际执行时机一般要比其设定的时间晚一些。**
- 刷新频率受 **屏幕分辨率** 和 **屏幕尺寸** 的影响，不同设备的屏幕绘制频率可能会不同，而 setTimeout 只能设置一个固定的时间间隔，这个时间不一定和屏幕的刷新时间相同。

以上两种情况都会导致 setTimeout 的执行步调和屏幕的刷新步调不一致，从而引起**丢帧**现象。

### 什么是requestAnimationFrame?

与setTimeout相比，**rAF**最大的优势是**由系统来决定回调函数的执行时机**。具体一点讲就是，**系统每次绘制之前会主动调用 rAF 中的回调函数**，如果系统绘制率是 60Hz，那么回调函数就每16.7ms 被执行一次，如果绘制频率是75Hz，那么这个间隔时间就变成了 1000/75=13.3ms。换句话说就是，rAF 的执行步伐跟着系统的绘制频率走。**它能保证回调函数在屏幕每一次的绘制间隔中只被执行一次**，这样就不会引起丢帧现象，也不会导致动画出现卡顿的问题。

以下是分别用js、react写的两个RAF的用法：

[js+RAF的用法](https://jsfiddle.net/studentHu/b670mk9g/)

[react+RAF 的基本用法](https://jsfiddle.net/studentHu/Lkd21osm/)

## 二、基于css3的简单动画

C3的基本思路还是定义好transition属性，然后通过react状态修改css属性值去实现

[React+CSS3动画](https://jsfiddle.net/studentHu/dx1pa548/)

基于 css3 的实现方式具有较高的性能，代码量少，但是只能依赖于 css 效果，对于复杂动画也很难实现。此外，通过修改 `state` 实现动画效果，只能作用于已经存在于 DOM 树中的节点。如果想用这种方式为组件添加入场和离场动画，需要维持至少两个 `state` 来实现入场和离场动画，其中一个 `state` 用于控制元素是否显示，另一个 `state` 用于控制元素在动画中的变化属性。在这种情况下，开发者需要花费大量精力来维护组件的动画逻辑，十分复杂繁琐。













连接参考

- https://www.cnblogs.com/onepixel/p/7078617.html
- https://tech.youzan.com/react-animations/
- https://www.zhangxinxu.com/wordpress/2013/09/css3-animation-requestanimationframe-tween-%E5%8A%A8%E7%94%BB%E7%AE%97%E6%B3%95/
- https://javascript.ruanyifeng.com/htmlapi/requestanimationframe.html