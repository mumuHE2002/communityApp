<template>
	<view class="flex align-center px-2 mb-1">
		<image :src="item.cover" style="width: 150rpx;height: 150rpx;"
		class="rounded mr-2"></image>
		<view class="flex flex-column">
			<text class="font-md">#{{item.title}}#</text>
			<text class="font text-secondary">{{item.desc}}</text>
			<view class="font text-secondary">
				<text class="mr-1">动态{{item.news_count}}</text>
				<text>今日{{item.today_count}}</text>
			</view>
		</view>
	</view>
</template>

<script>
	export default{
		props:{
			item:Object,
			index:Number
		}
	}
</script>

<style>
</style>
