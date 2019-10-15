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
			products: []
		},
		created () {
			fetch('https://api.myjson.com/bins/74163')
				.then(response => response.json())
				.then(json => {
					this.products = json.products
				})
		}
	})
</script>

```