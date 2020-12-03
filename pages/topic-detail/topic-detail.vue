<template>
	<view>
		<topic-info :info="info"></topic-info>
		<divider></divider>
		
		<view class="p-2 flex align-center border-bottom"
		hover-class="bg-light"
		 v-for="item in hotList" :key="item">
			<text class="iconfont icon-faxian text-main"></text>
			<view class="font text-dark text-ellipsis">
				{{item.title}}
			</view>
		</view>
		<divider></divider>
	</view>
</template>

<script>
	import topicInfo from '@/components/topic-detail/topic-info.vue';
	export default {
		components:{
			topicInfo
		},
		data() {
			return {
				info:{},
				hotList:[{
					title:"【新人必读】uni-app实在第二季商城类app开发(全栈)"
				},{
					title:"【升职必读】uni-app实在第三季模仿微信app开发(全栈)"
				}]
			}
		},
		onLoad(option) {
			this.info = option.detail && JSON.parse(option.detail)
		},
		methods: {
			
		}
	}
</script>

<style>
.filter{
	filter: blur(10px);
}
</style>
