Video's code

```
<div id="app">
	<ul>
		<li v-for="product in products">
			{{ product }}
		</li>
	</ul>
</div>

<script src="https://unpkg.com/vue"></script>
<script>
	const app = new Vue({
		el: '#app',
		data: {
			products: [
				'Boots',
				'Jacket',
				'Hiking Socks'
			]
		}
	})
</script>

```