<template>
	<view>
		<uni-list-item title="账户与安全" @click="open('user-password')">
			<text slot='footer' class="iconfont icon-jinru"></text>
		</uni-list-item>
		<uni-list-item title="绑定邮箱" @click="open('user-email')">
				<text slot='footer' class="iconfont icon-jinru"></text>
		</uni-list-item>
		<uni-list-item title="编辑资料" @click="open('user-userinfo')">
				<text slot='footer' class="iconfont icon-jinru"></text>
		</uni-list-item>
		<uni-list-item title="清楚缓存" @click="clear">
			<view class=" font-sm text-muted" slot="footer">
				{{currentSize | format}}
			</view>
		</uni-list-item>
		<uni-list-item title="意见反馈" @click="open('user-feedback')">
				<text slot='footer' class="iconfont icon-jinru"></text>
		</uni-list-item>
		<uni-list-item title="关于社区" @click="open('about')">
				<text slot='footer' class="iconfont icon-jinru"></text>
		</uni-list-item>
		
		<view class="p-2">
			<button class="bg-main text-white " style="border-radius: 50px;">退出登录</button>
		</view>
	</view>
</template>

<script>
	import uniListItem from '@/components/uni-components/uni-list-item/uni-list-item.vue';
	export default {
		components:{
			uniListItem
		},
		data() {
			return {
				currentSize:0
			}
		},
		onLoad() {
			this.getStorageInfo()
		},
		methods: {
			getStorageInfo() {
				const res = uni.getStorageInfoSync()
				this.currentSize = res.currentSize
			},
			open(path) {
				uni.navigateTo({
					url:`/pages/${path}/${path}`
				})
			},
			
			/* 清楚缓存 */
			clear() {
				uni.showModal({
					content:'是否清楚缓存',
					cancelText:'不清除',
					confirmText:'清除'
				}).then(res => {
					if(res[1]) {
						res = res[1]
						if(res.confirm) {
							uni.clearStorageSync()
							this.getStorageInfo()
							uni.showToast({
								title:'清除成功'
							})
						}
					}
				})
			}
		},
		filters:{
			format(v) {
				return v > 1024 ? (v / 1024).toFixed(2) +'MB' : v.toFixed(2) + 'KB'
			}
		}
	}
</script>

<style>

</style>
