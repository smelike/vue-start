
## 调用 element 中 el-form 的自定义校验规则

> 定义 validator

```
<template>
	<el-form :model="ruleForm" :rules="rules" ref="ruleForm">
		<el-form-item  prop="content">
			<el-input type="textarea" v-model.trim="ruleForm.content" :autosize="{ minRows: 3, maxRows: 5}" placeholder="发表评论(按Enter发送)" @keydown.enter.native="postComment"></el-input>
		</el-form-item>
	</el-form>
</template>

<script>
	export default {
		name: 'memo-detail',
		data () {
			var validateContent = (rul, val, callback) => {
				if (val === '') {
					callback(new Error('Please input comment-content'))
				} else {
					if (this.ruleForm.content !== '') {
						this.$refs.ruleForm.validateField('content')
					}
					callback()
				}
			}
			return {
				ruleForm: {
					content: ''
				},
				rules: {
					content: [
						{ validator: validateContent }
					]
				}
			}
		},
		mounted () {
			// ...
		},
		methods: {
			async postComment () {
				this.$refs.ruleForm.validate((valid) => {
					if (valid) {
						console.log('Okay, submit!')
					} else {
						console.log('Validate failed')
						return false
					}
				})
			}
		}
	}
</script>

```