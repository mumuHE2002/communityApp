<template>
	<view>
		<view class="p-2">
			<input class="input" type="text" placeholder="请输入你要绑定的邮箱" v-model="email" />
			<input class="input" type="text" placeholder="请输入密码" v-model="pwd" />

		</view>
		<button class="bg-main text-white m-2" style="border-radius: 50px;" 
		@click="submit" :disabled="disabled">设置</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				email: '',
				pwd: ''
			}
		},
		methods: {
			check() {
				const rule = /^([a-zA-Z]|[0-9])(\w|\-)+@[a-zA-Z0-9]+\.([a-zA-Z]{2,4})$/
				if(!rule.test(this.email)) {
					uni.showToast({
						title:'邮箱错误',
						icon:'none'
					})
					
					return false
				}
				
				return true
			},

			//监听提交
			submit() {
				if(!this.check()) return

				console.log('ok')
			}
		},
		computed:{
			disabled() {
				return this.email == '' || this.pwd == ''
			}
		}
	}
</script>

<style>
	.input {
		padding: 20rpx;
		border-bottom: 1px solid #C0C0C0;
	}
</style>
