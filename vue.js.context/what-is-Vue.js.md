是什么？

- 一套用于构建用户界面的渐进式框架。

- 被设计为可以自底向上逐层应用。

- Vue的核心库只关注视图层

Vue.js 的核心是一个允许采用`简洁的模板语法`来声明式地将数据渲染进 DOM 的系统：


> 声明式渲染

```
<div id="app">
	{{ message }}
</div>

<script>
	var app = new Vue({
		el: '#app',
		data: {
			message: 'Hello Vue!'
		}
	})
</script>
```

> 绑定元素特性: v-bind

```
<div id="app">
	<span v-bind:title="message">
	Mouse hover check the info.
	</span>
</div>

<script>
	var app = new Vue({
		el； '#app',
		data: {
			message: 'loading at ' + new Date().toLocalString()
		}
	})
</script>
```

> v-for



