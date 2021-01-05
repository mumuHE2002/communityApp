<template>
	<view>
		<navigator url="../login/login">
		<view class="flex align-center p-4" hover-class="bg-light" >
			<image src="/static/demo/userpic/14.jpg" 
			style="width: 100rpx;height: 100rpx;"
			class="rounded-circle mr-2"></image>
			<view class="flex flex-column justify-between flex-1">
				<view class="font-weight-bold font-md">123123</view>
				<view class="font text-secondary">
					<text class="mr-2">总帖子 1</text>
					<text>今日发帖 0</text>
				</view>
			</view>
			<text class="iconfont icon-jinru "></text>
		</view>
		</navigator>
		<view class="flex px-4">
			<block v-for="(item,index) in myData" :key='index'>
				<view class="flex-1 flex-center flex-column">
					<view class="font-lg font-weight-bold">
						{{item.num}}
					</view>
					<view class="font text-secondary">
						{{item.text}}
					</view>
				</view>
			</block>
		</view>
		
		<view class="px-4 py-2">
			<image src="/static/demo/banner2.jpg" mode="aspectFill"
			style="height: 170rpx;width: 100%;" class="rounded"></image>
		</view>
		
	<view class="px-2">
		<uni-list-item title="浏览历史" showExtraIcon >
			<text slot='icon' class="iconfont icon-liulan"></text>
			<text slot='footer' class="iconfont icon-jinru"></text>
		</uni-list-item>
		<uni-list-item title="社区认证" showExtraIcon>
			<text slot='icon' class="iconfont icon-huiyuanvip"></text>
			<text slot='footer' class="iconfont icon-jinru"></text>
		</uni-list-item>
		<uni-list-item title="审核帖子" showExtraIcon>
			<text slot='icon' class="iconfont icon-keyboard"></text>
			<text slot='footer' class="iconfont icon-jinru"></text>
		</uni-list-item>
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
				myData:[{
					text:'帖子',
					num:22
				},{
					text:'动态',
					num:2
				},{
					text:'评论',
					num:10
				},{
					text:'粉丝',
					num:3
				}]
			}
		},
		methods: {
	
		},
		onNavigationBarButtonTap() {
			uni.navigateTo({
				url:'/pages/user-set/user-set'
			})
		}
	}
</script>

<style>

</style>
