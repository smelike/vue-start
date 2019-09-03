模板语法


Vue.js 使用了基于 HTML 的模板语法

允许开发者声明式地将 DOM 绑定至底层 Vue 实例的数据。


在底层的实现上，Vue 将模板编译成虚拟 DOM 渲染函数。

结合响应系统，Vue 能智能计算出最少需要重新渲染多少组件，并把 DOM 操作次数减到最少。



# 插值 - {{ 属性名 }}

> 文本

数据绑定最常见的形式就是使用“Mustache”语法（双大括号）的文本插值：

```

<span>Message: {{ msg }}</span>

```

Mustache 标签将会被替代为对应数据对象上 msg 属性的值。

无论何时，绑定的数据对象上 msg 属性发生了改变，插值处的内容都会更新。


*v-once 指令，能执行一次性地插值，当数据改变时，插值处的内容不会更新。

**双大括号会将数据解释为普通文本，而非 HTML 代码。

**要输出真正的 HTML，需要使用 v-html 指令：

```
<p>Using mustaches: {{ rawHtml }}</p>

<p>Using v-html directive: <span v-html="rawHtml"></span></p>
```

----
这个 span 的内容将会被替换成为属性值 rawHtml，直接作为 HTML —— 会忽略解析属性值中的数据绑定。
注意，不能使用 v-html 来复合局部模板，因为 vue 不是基于字符串的模板引擎。
反之，对于用户界面(UI)，组件更适合作为可重用和可组合的基本单位。

> 站点上动态渲染的任意 HTML 可能会非常危险，因为它很容易导致 XSS 攻击。
> 请只对可信内容使用 HTML 插值，绝不要对用户提供的内容使用插值。

----

# 特性

Mustache 语法不能作用于 HTML 特性上，这种情况应该使用 v-bind 指令：

```

<div v-bind:id="dynamicId'></div>

```

对于布尔特性（只要存在就意味着值为 true）

```

<button v-bind:disabled="isButtonDisabled">Button</button>

```
> 如果 isButtonDisabled 的值是 null、undefined 或 false，则 disabled 特性甚至不会被包含在渲染出来的 <button> 元素中。


----

# 使用 JavaScript 表达式

```

{{ number + 1 }}

{{ ok ? 'YES' : 'No' }}

{{ message.split('').reverse().join('') }}

<div v-bind:id="'list-' + id"></div>

```

**有个限制，每个绑定都只能包含单个表达式，所以下面的例子都不会生效。

```
<!-- 这是语句，不是表达式 -->
{{ var a = 1 }}

<!-- 流控制也不会生效， 请使用三元表达式 -->

{{ if (ok) { return message } }}
```


----


# 指令

指令（Directives）是带有 v- 前缀的特殊特性。
指令特性的值预期是单个 JavaScript 表达式（v-for 是例外的）。

指令的职责是，当表达式的值改变时，将其产生的连带影响，响应式地作用于 DOM。

```
<p v-if="see">Now I get caught by you.</p>
```
> 这里，v-if 指令将根据表达式 seen 的值的真假来插入/移除 <p> 元素。


## 参数

```

// 将属性 href 与表达式 url 的值绑定
<a v-bind:href="url">...</a>


```
> v-on 指令，监听 DOM 事件

```
<a v-on:click="doSomething">Click me trigger the v-on-listener.</a>
```

### 动态参数

```
<a v-bind:[attributeName]="url">...</a>
```
当 Vue 实例有一个 data 属性 attributeName，其值为 "href"，那么这个绑定将等价于 v-bind:href。

```
<a v-bind:[eventName]="doSomething">...</a>
```
当 eventName 的值为 "focus" 时，v-on:[eventName] 将等价于 v-on:focus。



**如果在DOM 中使用模板（直接在一个 HTML 文件里撰写模板），
** 需要留意浏览器会把特性名全部强制转为小写：

```
<!-- 在 DOM 中使用模板是，会被转换为 `v-bind:[someattr]` -->

<a v-bind:[someAttr]="value">....</a>

```


### 修饰符

修饰符（modifier）是以半角句号 `.` 指明的特殊后缀，用于指出一个指令应该以特殊方式绑定。

例如， `.prevent` 修饰符告诉 `v-on` 指令对于触发的事件电泳 `event.preventDefault()` :

```
<form v-on:submit.prevent="obSumit">....</form>
```


### 指令缩写

> v-bind 

```
<!-- 完整语法 -->
<a v-bind:href="url">...</a>

<!-- 缩写 -->
<a :href="url">...</a>

```

> v-on

```
<!-- 完整语法 -->
<a v-on:click="doSomething">Click me will trigger something wonderful.</a>

<!-- for short -->
<a @click="doSomething">Click me will trigger something wonderful.</a>
```

