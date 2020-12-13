<template>
	<view class="">
		<!-- 时间 -->
		<view v-if="shortTime" class="py-2 flex-center font-sm text-light-muted">
			{{shortTime}}
		</view>
		<!-- 消息气泡 -->
		<view class="flex align-start p-2 " :style="isSelf?'flex-direction: row-reverse;':''">
			<image :src="item.avatar" style="width: 90rpx;height: 90rpx;" class="rounded-circle"></image>
			<view class="p-2 bg-light font rounded mx-2" style="max-width: 420rpx;">
				{{item.data}}
			</view>
		</view>
	</view>
</template>

<script>
	
	import $T from'@/common/time.js'
	
	export default{
		props:{
			item:Object,
			index:Number,
			uid:Number,
			pretime:[Number,String]
		},
		computed:{
			//是否本人的消息
			isSelf(){
				return this.uid === this.item.user_id
			},
			//转换时间
			shortTime() {
				return $T.getChatTime(this.item.create_time,this.pretime)
			}
		}
	}
</script>

<style>
</style>
