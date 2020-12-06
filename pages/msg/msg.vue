<template>
	<view>
		<!-- 消息列表 -->
		<template v-if="list.length > 0">
		<block v-for="(item,index) in list" :key='index'>
			<msg-list :item="item" :index="index"></msg-list>
		</block>
		</template>
		<template v-else>
			<no-thing></no-thing>
		</template>
		
	</view>
</template>

<script>
	const demo = [{
					avatar:"/static/demo/userpic/17.jpg",
					userNmae:"木木233",
					updateTime:1607268250,
					data:"s算卦的动手动脚师傅",
					noread:20
				},{
					avatar:"/static/demo/userpic/16.jpg",
					userNmae:"木木233",
					updateTime:1606033250,
					data:"s阿斯弗hdsfiiidjmdjm",
					noread:20
				},{
					avatar:"/static/demo/userpic/18.jpg",
					userNmae:"i速度与",
					updateTime:1607068250,
					data:"s啊速度京东方呼呼呼呼回复对方",
					noread:99
				}]
	import msgList from '@/components/msg/msg-list.vue'
	import noThing from '@/components/common/no-thing.vue'
	export default {
		components:{
			msgList,
			noThing
		},
		data() {
			return {
				list:[]
			}
		},
		onLoad() {
			this.list = demo
		},
		methods: {
			//下拉刷新
			refresh(){
				setTimeout(()=>{
					this.list = demo
					//停止下拉刷新状态
					uni.stopPullDownRefresh()
				},2000)
			}
		},
		//监听下拉刷新
		onPullDownRefresh() {
			this.refresh()
		},
	}
</script>

<style>

</style>
