Class 与 Style  绑定


### 对象语法

v-bind:class

```
<div v-bind:class="{ active: isActive }"></div>
```
> 上面的语法表示 active 这个 class 存在与否将取决于数据属性 isActive 的 truthiness。

可以在对象中传入更多属性来动态切换多个 class。此外，v-bind:class 指令也可以与普通的 class 属性共存。

有如下模板：

```
<div
class="static"
v-bind:class="{ active: isActive, 'text-danger': hasError }"
></div>

```

### 绑定的数据对象不必内联定义在模板里：

```
<div v-bind:class="classObject">
</div>
```
> JavaScript-Code

```
data: {
	classObject: {
		active: true,
		'text-danger': false
	}
}
```

### 绑定一个返回对象的计算属性

```

<div v-bind:class="classObject"></div>

data: {
	isActive: true,
	error: null
},
computed: {
	classObject: function () {
		return {
			active: this.isActive && !this.error,
			'text-danger': this.error && this.error.type === 'fatal'
		}
	}
}

```


### 数组语法

把一个数组传给 v-bind:class ，以应用一个 class 列表：

```
<div v-bind:class="[activeClass, errorClass]"></div>

data: {
	activeClass: 'active',
	errorClass: 'text-danger'
}
```

渲染为：

```
<div class="active text-danger"></div>
```


> 根据条件切换列表中的 class，可以用三元表达式：

```
<div v-bind:class="[isActive ? activeClass: '', errorClass]"></div>
```

当有多个条件 class 时，这样写有些繁琐。所以在数组语法中也可以使用对象语法：

```
<div v-bind:class="[{  active: isActive }, errorClass]"></div>
```


**当在一个自定义组件上使用 class 属性时**，这些类将被添加到该组件的根元素上面。这个元素上已经存在的类不会被覆盖。


> 声明组件

```
Vue.component('my-component', {
	template: '<p class="foo bar">Hi</p>'
})
``` 

> 再使用时添加一些 class：

```
<my-component lcass="bass boo"></my-component>
```

渲染结果：

```
<p class="foo bar baz bass boo">Hi</p>
```


对于带数据绑定 class 也同样适用：

```
<my-component v-bind:class="{ active: isActive }"></my-component>
```

当 isActive 为 truthy 时，渲染结果：

```
<p class="foo bar active">Hi</p>
```

### 绑定内联样式

```
<div v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>

data: {
  activeColor: 'red',
  fontSize: 30
}
```

直接绑定一个样式对象：


```
<div v-bind:style="styleObject"></div>

data: {
	styleObject: {
		color: 'red',
		fontSize: '13px'
	}
}
```

### 多个对象的数组语法

```
<div v-bind:style="[baseStyles, overridingStyles]"></div>
```

当 **v-bind:style** 使用需要添加浏览器引擎前缀的 CSS 属性时，如 **transform**， Vue.js 会自动侦测并添加相应的前缀。


### 多重值

从 2.3.0 起你可以为 style 绑定中的属性提供一个包含多个值的数组，常用于提供多个带前缀的值，例如：

<div :style="{ display: ['-webkit-box', '-ms-flexbox', 'flex'] }"></div>

这样写只会渲染数组中最后一个被浏览器支持的值。在本例中，如果浏览器支持不带浏览器前缀的 flexbox，那么就只会渲染 display: flex。


译者注
[1] truthy 不是 true，详见 MDN 的解释。
