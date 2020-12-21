<template>
	<view>
		<uni-list-item title="账户与安全">
			<text slot='footer' class="iconfont icon-jinru"></text>
		</uni-list-item>
		<uni-list-item title="编辑资料">
				<text slot='footer' class="iconfont icon-jinru"></text>
		</uni-list-item>
		<uni-list-item title="清楚缓存">
				<text slot='footer' class="iconfont icon-jinru"></text>
		</uni-list-item>
		<uni-list-item title="意见反馈">
				<text slot='footer' class="iconfont icon-jinru"></text>
		</uni-list-item>
		<uni-list-item title="关于社区">
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
				
			}
		},
		methods: {
			
		}
	}
</script>

<style>

</style>
