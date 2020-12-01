<template>
	<view>
		<view class="flex align-center justify-between px-2">
			<view class="font-md">热门分类</view>
			<view class="font text-light-muted animated" hover-class="jello" @click="openMore">
				更多
				<text class="iconfont icon-jinru"></text>
			</view>
		</view>
		<view class="flex align-center justify-between px-2 py-3 border-bottom">
			<view class="border-gray rounded px-2 bg-gray animated" :hover-class="'jello'" 
			v-for="(item,index) in hotCate" :key="index" @click="openDetail(item)">{{item.name}}</view>
		</view>
	</view>
</template>

<script>
	export default {
		props:['hotCate'],
		methods:{
			openMore(){
				this.$emit('openMore')
			},
			openDetail(item) {
				console.log('打开详情')
			},
		}
	}
</script>

<style>
</style>
