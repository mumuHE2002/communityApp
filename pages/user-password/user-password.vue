<template>
	<view class="p-2">
		<input class="input" type="text" placeholder="输入旧密码"
		 v-model="oldpwd"/>
		<input class="input" type="text" placeholder="输入新密码" 
		v-model="newpwd"/>
		<input class="input" type="text" placeholder="请确认密码" 
		v-model="renewpwd"/>
		<view class="p-2">
			<button class="bg-main text-white " 
			style="border-radius: 50px;"
			:disabled='disabled' @click="submit">设置</button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				oldpwd:"",
				newpwd:"",
				renewpwd:''
			}
		},
		methods: {
			//验证
			check() {
				if(this.newpwd !== this.renewpwd) {
					uni.showToast({
						title:'两次输入密码不一致',
						icon:'none'
					})
					return false
				}
				
				return true
			},
			
			//监听提交
			submit() {
				if(!this.check()) return false
				
				console.log('ok')
			}
		},
		computed:{
			disabled() {
				return this.oldpwd == '' || this.newpwd == '' || this.renewpwd == ''
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
