# react-router



## 1.基本用法

```javascript
import { Router, Route, hashHistory } from 'react-router'

render((
	<Router history={hashHistory}>
  <Route path="/" component={App}/>
  <Route path="/repos" component={Repos}/>
  <Route path="/about" component={About}/>
</Router>
),document.getElementById('app'));
```



