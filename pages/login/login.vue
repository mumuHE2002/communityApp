<template>
	<view>
		<uni-nav-bar :border='false'></uni-nav-bar>
		<view>
			<view class="iconfont icon-guanbi flex-center font-lg font-weight-bold" hover-class="text-main" @click="back" style="width: 100rpx;height: 100rpx; "></view>
		</view>

		<template v-if="!status">
			<view class="text-center" style="padding-top: 130rpx;padding-bottom: 70rpx; font-size: 50rpx;">
				账户密码登录
			</view>

			<view class="p-2">
				<view class="mb-2">
					<input type="text" class="border-bottom p-2" v-model="uname" placeholder="昵称/手机号/邮箱" />
				</view>
				<view class="mb-2 flex">
					<input type="text" class="border-bottom p-2 flex-1" v-model="pwd" placeholder="请输入密码" />
					<view class="flex-center font text-muted border-bottom" style="width: 140rpx;">忘记密码?</view>
				</view>
			</view>
		</template>

		<template v-else>
			<view class="text-center" style="padding-top: 130rpx;padding-bottom: 70rpx; font-size: 50rpx;">
				手机验证码登录
			</view>

			<view class="p-2">
				<view class="mb-2 flex">
					<view class="flex-center border-bottom font-weight-bold" style="width: 80rpx;">+86</view>
					<input type="text" class="border-bottom p-2 flex-1" v-model="phone" placeholder="昵称/手机号/邮箱" />
				</view>
				<view class="mb-2 flex">
					<input type="text" class="border-bottom p-2 flex-1" v-model="code" placeholder="请输入验证码" />
					<view class="flex-center font text-white bg-main border-bottom" 
					@click="getCode"
					style="width: 180rpx;">{{codeTime === 0 ? '获取验证码' : codeTime+' s'}}</view>
				</view>
			</view>
		</template>

		<view class="p-2">
			<button class="bg-main text-white " style="border-radius: 50px;" :disabled="disabled">登录</button>
		</view>

		<view class="flex-center py-4">
			<view class="text-primary font-sm" @click="changeStatus">
				{{status?'账户密码登录':'验证码登录'}}
			</view>
			<view class="text-muted mx-2">|</view>
			<view class="text-primary font-sm">登录遇到问题</view>
		</view>

		<view class="flex-center py-3">
			<view class="bg-secondary" style="height: 1rpx;width: 100rpx;"></view>
			<view class="font-sm text-secondary mx-2">社交账户登录</view>
			<view class="bg-secondary" style="height: 1rpx;width: 100rpx;"></view>
		</view>

		<other-login></other-login>

		<view class="flex-center text-muted font-sm py-2">
			注册及代表同意<text class="text-primary">《木木社区协议》</text>
		</view>
	</view>
</template>

<script>
	import uniNavBar from '@/components/uni-components/uni-nav-bar/uni-nav-bar.vue';
	import otherLogin from '@/components/common/other-login.vue';
	export default {
		components: {
			uniNavBar,
			otherLogin
		},
		data() {
			return {
				status: false,
				uname: '',
				pwd: '',
				phone: '',
				code: '',
				
				codeTime:0
			}
		},
		onLoad() {

		},
		methods: {
			back() {
				uni.navigateBack({})
			},

			/* 切换登录方式 */
			changeStatus() {
				this.initForm()
				this.status = !this.status
			},
			
			/* 初始化表单 */
			initForm() {
				this.uname =''
				this.pwd = ''
				this.phone = ''
				this.code = ''
			},
			
			/* 获取验证码 */
			getCode() {
				if(this.codeTime > 0) {
					return false
				}
				
				this.codeTime = 10
				const timer = setInterval(()=>{
					this.codeTime--
					if(this.codeTime <= 0) {
						clearInterval(timer)
					}
				},1000)
			}
		},
		computed: {
			disabled() {
				if ((this.uname === '' || this.pwd === '') && (this.phone === '' || this.code === '')) {
					return true
				} else {
					return false
				}
			}
		}
	}
</script>

<style>

</style>
