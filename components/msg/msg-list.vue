<template>
	<view class="py-2 mx-2 flex align-center border-bottom border-light-secondary" hover-class="bg-light">
		<image :src="item.avatar" class="rounded-circle mr-2" style="width: 80rpx;height: 80rpx;"></image>
		<view class="flex flex-column flex-1">
			<view class="flex align-center justify-between">
				<text class="font-md">{{item.userNmae}}</text>
				<text class="font-sm text-secondary">
				{{item.updateTime | formatTime}}</text>
			</view>
			<view class="flex align-center justify-between">
				<text class="text-secondary text-ellipsis" style="width: 500rpx;">{{item.data}}</text>
				<uni-badge :text="item.noread" :type="'error'" size="small"></uni-badge>
			</view>
		</view>
	</view>
</template>

<script>
	import uniBadge from "@/components/uni-components/uni-badge/uni-badge.vue" 
	import $T from '@/common/time.js'
	export default{
		components:{
			uniBadge
		},
		props:{
			item:Object,
			index:Number
		},
		filters:{
			formatTime(value) {
				return $T.gettime(value)
			}
		},
	}
</script>

<style>
</style>
