# JavaScript Basic
true \ [] \ {}

false \ 0 \ '' \ ""


# Browser-Console 
Console 中通过 \ 来进行换行

# JavaScript Functions

Array.push()
Array.shift()


# vue 指令

v-bind
v-if
v-for

监听事件
v-on: 
v-on:click="eventFunctionName"

v-model  实现表单输入和应用状态之间的双向


# 组件化应用构建

组件系统是 Vue 的另一个重要概念。它是一种抽象，允许使用小型、独立和可复用的组件构建大型应用。
几乎任意类型的应用界面都可以抽象为一个组件树。

> 注册组件

```
Vue.component('todo-item', {
	template: '<li>This is an todo-item.</li>'
})
```

> 使用它构建另一组件模板

```
<ol>
	<!-- 创建 todo-teim 组件的实例 -->
	<todo-teim></todo-item>
</ol>
```

> 每个待办项是不同的文本才对，我们应该能从父作用域将数据传到子组件才对。

```
Vue.component('todo-item', {
	// todo-item 组件现在接受一个
	// "prop"，类似于一个自定义特性。
	// 这个 prop 名为 todo。
	props:['todo'],
	template: '<li>{{ todo.text }}</li>'
})
```

> 使用 v-bind 指令将待办事项传到循环输出到每个组件中

```
	<div id="app-7">
		<ol>
			<!--
				todo-item 提供 todo 对象，todo 对象是变量，即其内容可以是动态的。
				也需要为每个组件提供一个 "key"
			-->
			<todo-item
				v-for="item in groceryList"
				v-bind:todo="item"
				v-bind:key="item.id"
			>
			</todo-item>
		</ol>
	</div>
	
	Vue.component('todo-item', {
		props: ['todo'],
		template: '<li>{{ todo.text }}</li>'
	})
	var app7 = new Vue({
		el: '#app7',
		data: {
			groceryList: [
				{ id: 0, text: 'vegetable' },
				{ id: 1, text: '奶酪' },
				{id: 2, text: 'something whatever' }
			]
		}
	})
```

> 子单元通过 prop 接口与父单元进行了良好的解耦。还可以进一步改进 <todo-item> 组件，提供更为复杂的模板和逻辑，而不会影响到父单元。



# 一个假想的例子，展示使用了组件的应用模板是什么样的：

```
<div id="app">
	<app-nav></app-nav>
	<app-view>
		<app-siderbar></app-sidebar>
		<app-content></app-content>
	</app-view>
</div>

```