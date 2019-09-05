truthy(真值)


https://developer.mozilla.org/zh-CN/docs/Glossary/Truthy


在 JavaScript 中，truthy（真值）指的是在布尔值上下文中，转换后的值为真的值。所有值都是真值，除非它们被定义为 假值（即除 false、0、""、null、undefined 和 NaN 以外皆为真值）。

JavaScript 在布尔值上下文中使用强制类型转换（coercion）。

JavaScript 中的真值示例如下（将被转换为 true，if 后的代码段将被执行）：


```
if (true)
if ({})
if ([])
if (42)
if ("foo")
if (new Date())
if (-42)
if (3.14)
if (-3.14)
if (Infinity)
if (-Infinity)

```


