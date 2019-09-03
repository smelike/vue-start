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

