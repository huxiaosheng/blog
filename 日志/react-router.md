# react-router



## 1.基本用法

```javascript
import { Router, Route, hashHistory } from 'react-router'

render((
	<Router history={hashHistory}>
  <Route path="/" exact component={App}/>
  <Route path="/repos" component={Repos}/>
  <Route path="/about" component={About}/>
</Router>
),document.getElementById('app'));
```



**exact**

精准匹配，只有完全等于这个路由才会显示相应页面