## 条件渲染


v-if 指令永固条件性地渲染一块内容。

这块内容智慧在指令的表达式返回 truthy 值的时候被渲染。


> JavaScript-Code-#1

```

<h1 v-if="awesome">Vue is awesome!</h1>

```


> JavaScript-Code-#2

```
<h1 v-if="awesome">Vue is awesome!</h1>
<h1 v-else>Ob no smile..</h1>
```

**v-if** 是一个指令，所以必须将它添加到一个元素上。

切换多个元素呢？可以把一个 **<template>** 元素当做不可见的包裹元素，并在上面使用 **v-if**。


### v-else

可以使用 **v-else** 指令来表示 **v-if** 的 "else块":

```
<div v-if="Math.random() > 0.5">
	Now You see me
</div>
<div v-else>
	Now You don't
</div>
```

**v-else** 元素必须跟随在在 **v-if** 或者 **v-else-if** 的元素的后面。


### v-else-if

v-else-if 也必须紧跟在带 v-if 或者 v-else-if 的元素之后。


### 用 key 管理可复用的元素

vue 会尽可能高效地渲染元素，通常会复用已有元素而不是从头开始渲染。

案例代码如下：

```
<template v-if="loginType ==='username'">
	<label>Username</label>
	<input placeholder="Enter your name" />
</template>
<template v-else>
	<label>Email</label>
	<input placeholder="Enter your email address">
</template>
```

### 告诉 Vue 这两个元素时完全嘟列，不要复用它们。

只需添加一个具有唯一值得 **key** 属性即可。

```
<input placeholder="Enter your name" key="username-input" />

<input placeholder="Enter your email" key="email-input" />
```

----

### v-show 根据条件展示元素的选项

```
<h1 v-show="ok">Hello!!</h1>
```

不同的是带有 **v-show** 的元素始终会被渲染并保留在 DOM 中。 **v-show** 只是简单地切换元素的 CSS 属性 **display**。

**v-show** 不支持 **<template>** 元素，也不支持 **v-else**


----

### v-if VS v-show

v-if 是“真正”的条件渲染，因为它会确保在切换过程中，条件块内的事件监听器和子组件适当地被销毁和重建。

v-if 也是惰性的：如果在初始渲染时条件为假，则什么也不做——直到条件第一次变为真时，才会开始渲染条件块。

v-show ，元素总是会被渲染，并且只是简单地基于 CSS 进行切换。

v-if 有更高的切换开销，而 v-show 有更高的初始渲染开销。

非常频繁地切换，则使用 **v-show** 较好；如果在运行时条件很少改变，则使用 **v-if** 较好。



### v-if 与 v-for

不推荐同时使用 **v-if** 和 **v-for**

当 v-if 与 v-for 一起使用时，v-for 具有比 v-if 更高的优先级。





