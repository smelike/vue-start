### deal with CORS error on Vue CLI 3


![How to deal with CORS erros on Vue CLI3](https://medium.com/js-dojo/how-to-deal-with-cors-error-on-vue-cli-3-d78c024ce8d3)

Create a `vue.config.js` file in the root of the frontend project right beside `package.json`, containing:

```
// vue.config.js
module.exports = {
	// options...
}
```



![devServer](https://cli.vuejs.org/config/#devserver-proxy)