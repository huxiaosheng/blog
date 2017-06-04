## controller

- 不要试图去复用controller,一个控制器一般只负责一小块视图
- 不要在Controller中操作DOM，这不是控制器的职责
- 不要在Controller里面左数据格式化，ng有很好的表单控件
- 不要在Controler里面左数据过滤操作，ng有$filter服务
- 一般来说，**Controller是不会互相调用的**，控制器之间的交互会通过事件进行





## mvc

**angular中的mvc全部是由$scope 作用域去实现的**



*Angular启动并生成视图是，ng-app元素同$rootScope进行绑定。*



$rootScope是所有 scope对象的最上层。*



### $scope

- 是一个js对象
- 提供了一些工具方法$watch()
- 是表达式的执行环境（或者叫作用域）
- 是一个树型结构，**与DOM标签平行**






## ngRoute進行視圖之間的路由

