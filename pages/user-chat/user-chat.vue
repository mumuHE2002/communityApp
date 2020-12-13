<template>
	<view>

		<!-- 聊天界面 -->
		<scroll-view scroll-y="true" 
		style="position: absolute; left: 0; top: 0; right: 0; bottom: 101rpx;"
		:scroll-into-view="scrollTnto" scroll-with-animation>
			<view>
				<block v-for="(item,index) in list" :key='index'>
					<view :id="'chat'+index">
						<user-chart-list :item="item" :index="index" :uid='uid' 
						:pretime="index > 0 ? list[index-1].create_time : 0"
						></user-chart-list>
					</view>
				</block>
			</view>
		</scroll-view>

		<!-- 底部操作条 -->
		<view id="a" class="fixed-bottom flex align-center border-top border-light bg-white" style="height: 100rpx;">
			<input class="flex-1 bg-light rounded ml-2 py-1 px-2 font" 
			type="text" placeholder="文明发言" v-model="content" @confirm='submit'/>
			<view class="iconfont icon-fabu font-lg flex-center animated" 
			hover-class="jello text-main" style="width: 100rpx;"
			@click="submit"></view>
		</view>
	</view>
</template>

<script>
	const demo = [{
		user_id: 1,
		avatar: "/static/demo/userpic/2.jpg",
		username: "昵称",
		data: "早上好呀！！吃早餐了吗？",
		type: "text",
		create_time: 1607815822
	}, {
		user_id: 2,
		avatar: "/static/demo/userpic/1.jpg",
		username: "昵称",
		data: "还没吃呢",
		type: "text",
		create_time: 1607817023
	}, {
		user_id: 1,
		avatar: "/static/demo/userpic/2.jpg",
		username: "昵称",
		data: "我在食堂，我帮你带一份吧！",
		type: "text",
		create_time: 1607817083
	}, {
		user_id: 1,
		avatar: "/static/demo/userpic/2.jpg",
		username: "昵称",
		data: "中午好呀！吃饭了吗？",
		type: "text",
		create_time: 1607832000
	}, {
		user_id: 1,
		avatar: "/static/demo/userpic/2.jpg",
		username: "昵称",
		data: "下午好，吃饭了没，我请你火锅去",
		type: "text",
		create_time: 1607853600
	}, {
		user_id: 1,
		avatar: "/static/demo/userpic/2.jpg",
		username: "昵称",
		data: "晚上好，你咋不回我消息？",
		type: "text",
		create_time: 1607873400
	}, {
		user_id: 1,
		avatar: "/static/demo/userpic/2.jpg",
		username: "昵称",
		data: "晚安",
		type: "text",
		create_time: 1607875199
	}, {
		user_id: 1,
		avatar: "/static/demo/userpic/2.jpg",
		username: "昵称",
		data: "晚安",
		type: "text",
		create_time: 1607875199
	}, {
		user_id: 1,
		avatar: "/static/demo/userpic/2.jpg",
		username: "昵称",
		data: "晚安",
		type: "text",
		create_time: 1607875199
	}, {
		user_id: 1,
		avatar: "/static/demo/userpic/2.jpg",
		username: "昵称",
		data: "晚安",
		type: "text",
		create_time: 1607875199
	}, {
		user_id: 1,
		avatar: "/static/demo/userpic/2.jpg",
		username: "昵称",
		data: "晚安",
		type: "text",
		create_time: 1607875199
	}]

	import userChartList from '@/components/user-chat/user-chat-list.vue'
	export default {
		components: {
			userChartList
		},
		data() {
			return {
				uid: 1,
				content:"",
				list: [],
				scrollTnto:""
			}
		},
		onLoad() {
			this.list = demo
		},
		onReady() {
			this.pageToBottom()
		},
		methods: {
			//发送
			submit() {
				let obj = {
					user_id: 1,
					avatar: "/static/demo/userpic/2.jpg",
					username: "昵称",
					type: "text",
					data: this.content,
					create_time: (new Date()).getTime()
				}
				//判断是否输入内容
				if(this.content !== '') {
					this.list.push(obj)
					this.content = ''
					//滚动底部
					this.pageToBottom()
				}
			},
			
			//滚动底部
			pageToBottom() {
				let lastIndex = this.list.length - 1
				if(lastIndex < 0) return false
				this.scrollTnto = 'chat'+lastIndex
				console.log(this.scrollTnto)
			}
		}
	}
</script>

<style>

</style>
