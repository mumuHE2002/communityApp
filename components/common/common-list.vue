<template>
	<view class="p-2">
		<view class="flex align-center justify-between">
			<view class="flex align-center">
				<image class="rounded-circle mr-2" style="width: 65rpx; height: 65rpx;" :src="item.userpic" lazy-load @click="openSpace"></image>
				<view class="flex flex-column">
					<text class="font" style="line-height: 1.5;">{{item.username}}</text>
					<text class="font-sm text-light-muted" style="1.5">{{item.newstime}}</text>
				</view>
			</view>
			<view class="flex align-center justify-center rounded text-white bg-main animated faster" style="width: 90rpx; height: 50rpx;"
			 hover-class="jello" @click="follow" v-if="!item.isFollow">
				关注
			</view>
		</view>


		<!-- 标题 -->
		<view class="font-md my-1" @click="openDetail">
			{{item.title}}
		</view>
		<!-- 帖子详情 -->
		<slot>
			<!-- 图片 -->
			<block v-if="item.titlepic">
				<image class="rounded w-100-" style="height:350rpx " :src="item.titlepic" lazy-load @click="openDetail"></image>
			</block>
		</slot>
		<!-- 图标按钮 -->
		<!-- 顶 -->
		<view class="flex align-center">
			<view class="flex align-center justify-center flex-1 animated" hover-class="tada" @click="doSupport('support')"
			 :class="item.support.type === 'support' ? 'text-main' : ''">
				<text class="iconfont icon-dianzan2 mr-2"></text>
				<text>{{item.support.support_count || "顶"}}</text>
			</view>
			<!-- 踩 -->
			<view class="flex align-center justify-center flex-1 animated" hover-class="tada" @click="doSupport('unsupport')"
			 :class="item.support.type === 'unsupport'?'text-main':''">
				<text class="iconfont icon-cai mr-2"></text>
				<text>{{item.support.unsupport_count || "踩"}}</text>
			</view>
			<view class="flex align-center justify-center flex-1 animated" hover-class="tada text-main" 
			@click="doComment">
				<text class="iconfont icon-pinglun2 mr-2"></text>
				<text>{{item.comment_count || "评论"}}</text>
			</view>
			<view class="flex align-center justify-center flex-1 animated" hover-class="tada text-main" 
			@click="doShare">
				<text class="iconfont icon-zhuanfa1 mr-2"></text>
				<text>{{item.share_num || "分享"}}</text>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			item: Object,
			index:{
				type:Number,
				default: -1
			},
			isDetail: {
				type: Boolean,
				default: false
			}
		},
		data() {
			return {

			}
		},
		methods: {
			//打开个人空间
			openSpace() {
				console.log("OpenSpace")
			},

			//关注
			follow() {
				this.$emit("follow", this.index)
			},

			//进入详情页
			openDetail() {
				//如果是在详情页中，则不跳转
				if (this.isDetail) return false
				uni.navigateTo({
					url: '/pages/detail/detail?detail=' + JSON.stringify(this.item)
				})
			},

			//顶踩操作
			doSupport(type) {
				this.$emit("doSupport", {
					type,
					index: this.index
				})
			},
			//评论
			doComment() {
				if(!this.isDetail) return this.openDetail()
				
				this.$emit('doComment')
			},
			//分享
			doShare(){
				if(!this.isDetail) return this.openDetail()
				
				this.$emit('doShare')
			}
		}
	}
</script>

<style>
</style>
