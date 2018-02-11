# flux架构



## 基本概念

- View：视图层
- Action（动作）：视图层发出的消息（比如mouseClick）
- Dispatcher(派发器)：用来接收Actions、执行回调函数
- Store(数据层)：用来存放应用的状态，一旦发生变动，就提醒views要更新页面



