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
		
		<uni-popup type="top" ref="popup">
			<view class="bg-white ">
				<view class="flex-center border-bottom font-md py-2"
				hover-class="bg-light" @click="popupEvent('friend')">
					<text class="iconfont icon-sousuo mr-2"></text> 搜索好友
				</view>
				<view class="flex-center font-md py-2" hover-class="bg-light"
				@click="popupEvent('clear')">
					<text class="iconfont icon-qingchu mr-2 "></text> 清楚列表
				</view>
			</view>
		</uni-popup>
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
				}];
				
	import msgList from '@/components/msg/msg-list.vue'
	import noThing from '@/components/common/no-thing.vue'
	import uniPopup from '@/components/uni-components/uni-popup/uni-popup.vue'
	export default {
		components:{
			msgList,
			noThing,
			uniPopup
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
			},
			
			//弹出层点击事件
			popupEvent(e) {
				switch (e) {
					case 'friend':
						console.log('添加好友')
						break
					case 'clear':
						console.log('清楚列表')
						break
				}
				//关闭弹出层
				this.$refs.popup.close()
			}
		},
		//监听下拉刷新
		onPullDownRefresh() {
			this.refresh()
		},
		//监听原生导航按钮
		onNavigationBarButtonTap(e) {
			switch (e.index) {
				case 0:  //左边
					uni.navigateTo({url:'/pages/user-list/user-list'})
					this.$refs.popup.close()
					break
				case 1:
					this.$refs.popup.open()
					break
			}
		},
	}
</script>

<style>

</style>
