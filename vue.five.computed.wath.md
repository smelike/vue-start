计算属性和侦听器

computed attribute and watch

https://cn.vuejs.org/v2/guide/computed.html


模板中放入太多的逻辑，会令模板过重且难以维护。

例如：

```
<div id="example">
	{{ message.split('').reverse().join('') }}
</div>
```

> 模板不再是简单的声明式逻辑。你必须要看一段时间才能意识到，这里是想要显示变量 `message` 的翻转字符串.
> 当你想要在模板中多次引用此处的翻转字符串时，就会更加难以处理。
> 所以，对于任何复杂逻辑，你都应当使用**计算属性**。


### 基础例子

```
<div id="example">
	<p>Original message: "{{ message }}"</p>
	<p>Computed reversed message: "{{ reversedMessage }}"</p>
</div>
```
> JavaScript Code

```
var vm = new Vue({
	el: '#example',
	data: {
		message: 'Hello'
	},
	computed: {
		reversedMessage: function () {
			return this.message.split('').reverse().join('')
		}
	}
})
```

声明了一个计算属性 **reversedMessage**，提供的函数将用作属性 **vm.reversedMessage** 的 getter 函数。

你可以像绑定普通属性一样在模板中绑定计算属性。Vue 知道 **vm.reversedMessage** 依赖于 **vm.message**。
因此，当 **vm.message** 发生改变时，所有依赖 **vm.reversedMessage**的绑定也会更新。


### 计算属性缓存 vs 方法

可以通过在表达式中调用方法来达到同样的效果：

```
<p>Reversed message: “{{ reversedMessage() }}”</p>
```

> JavaScript - Code

```
methods: {
	reversedMessage: function () {
		return this.message.split('').reverse().join('')
	}
}

```

将同一函数定义为一个方法而不是一个计算属性。两种方式的最终结果确实是完全相同的。

然而，不同的是**计算属性是基于它们的响应式依赖进行缓存的。**

只在相关响应式依赖发生改变时，它们（指计算属性）才会重新求值。

这就意味着只要 message 还没有发生改变，多次访问 **reversedMessage**计算属性会立即返回【之前的计算结果】，而不必再次执行函数。

这意味着下面的计算属性将不再更新，因为 **Date.now()** 不是响应式依赖：

```
computed: {
	now: function () {
		return Date.now()
	}
}

```

相比之下，每当触发重新渲染时，调用方法将总会再次执行函数。

为什么需要缓存？假设有一个性能开销比较大的计算属性 A，需要遍历一个巨大的数组并做大量的计算。

然后我们可能有其他的计算属性依赖于 A。如果没有缓存，我们将不可避免的多次执行 A 的 getter。
而执行 A 的 getter 就会产生巨大的性能开销。所以我们需要缓存。

如果不希望有缓存，请用方法替代。


### 计算属性 vs 侦听属性

Vue 提供了一种更通用的方式来观察和响应 Vue 实例上的数据变动：**侦听属性。**
一些数据需要随着其他数据变动而变动时，很容易滥用 watch。
通常更好的做法是使用计算属性而不是命令式的 **watch**回调。

```
<div id="demo">{{ fullName }}</div>
```
> JavaScript Code

```
var vm = new Vue({
	el: '#demo',
	data: {
		firstName: 'Foo',
		lastName: 'Bar',
		fullName: 'Foo Base'
	},
	watch: {
		firstName: function (val) {
			this.fullName = val + ' ' + this.lastName
		},
		lastName: function (val) {
			this.fullName = this.firstName + ' ' + val
		}
	}
})
```

> 计算属性的版本进行比较：

```
var vm = new Vue({
	el: '#demo',
	data: {
		firstName: 'Foo',
		lastName: 'Bar'
	},
	computed: {
		fullName: function () {
			return this.firstName + ' ' + this.lastName
		}
	}
})

```


### 计算属性的 setter

计算属性默认只有 getter，需要时你也可以提供一个 setter：

```
// ...
computed: {
	fullName: {
		// getter
		get: function () {
			return this.firstName + ' ' + this.lastName
		},
		// setter
		set: function (newValue) {
			var names = newValue.split(' ')
			this.firstName = names[0]
			this.lastName = names[names.lenght - 1]
		}
	}
}

// ...
```


### 侦听器

计算属性在大多数情况下更合适，但有时也需要一个自定义的侦听器。

当需要在数据变化时执行异步或开销较大的操作时，这个方式是最有用的。










