<template>
	<view>
		<view class="flex-center flex-column pt-4 pb-3">
			<image src="../../static/demo/nothing.jpg"  class="rounded-circle"
			style="height: 150rpx;width: 150rpx;"></image>
			<text class="font text-muted mt-2">version 1.0.1</text>
		</view>
		
		<uni-list-item title="新版本检查" link></uni-list-item>
		<uni-list-item title="社区用户协议" link></uni-list-item>
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
