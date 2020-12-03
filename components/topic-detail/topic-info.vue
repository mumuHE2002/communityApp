<template>
	<view>
		<view class="position-relative">
			<image :src="info.cover" mode="aspectFill" 
			class="w-100 filter" style="height: 300rpx;"></image>
		</view>
		<view class="bg-white position-relative px-2 pb-2" style="z-index: 10;">
			<view class="flex">
				<image :src="info.cover" 
				style="width: 150rpx;height: 150rpx; margin-top: -75rpx;" class="rounded mr-2"></image>
				<view class="font-md">
					#{{info.title}}#
				</view>
			</view>
			<view class="flex font text-secondary my-2">
				<view class="mr-2">动态{{info.news_count}}</view>
				<view class="">今日{{info.today_count}}</view>
			</view>
			<view class="font-md text-secondary ">{{info.desc}}</view>
		</view>
	</view>
</template>

<script>
	export default{
		props:{
			info:Object
		}
	}
</script>

<style>
</style>
