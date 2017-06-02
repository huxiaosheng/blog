# EventEmitter 类

Node.js 所有的一步I/O操作在完成时都会发送一个事件到事件队列。

Node.js里面的很多对象都会分发事件：一个net.Server对象会在每次有新连接时分发一个事件，一个fs.readStream对象会在文件被打开的时候发出一个事件。所有这些产生事件的对象都是events.EventEmitter的实例



```javascript
//引入 events 模块
var events = require('events');

//创建 eventEmitter 对象
var eventEmitter = new events.EventEmitter();

```

