
#创建 vue 实例

```
var vm = new Vue({
	// 选项
})
```

创建一个 Vue 实例，可以传入一个选项对象。该选项对象是用来创建你想要的行为。



# 数据与方法

当一个 Vue 实例被创建时，它将 data 对象中所有的属性加入到 Vue 的响应式系统中。
当这些属性的值发生改变时，视图将会产生“响应”，及匹配更新为新的值。


当data 中的数据改变时，视图会进行重渲染。

注意：只有当实例被创建时 data 中存在的属性才是响应式的。（响应式指的视图与数据改变是同步的）

> 添加一个新的属性 b

```
vm.b = hi''
```

对 b 的改动将不会触发任何视图的更新。

