<template>
	<view>
		<view class="">
		
		<template v-if="searchData.length === 0">
			<view class="font-md mx-2">
				搜索历史
			</view>
			<view class="flex flex-wrap">
				<view class="border rounded px-2 mx-2 my-1 "
				 v-for="(item,index) in list" :key="index"
				 hover-class="bg-light" @click="clickSearchHistory(item)"
				>{{item}}</view>
			</view>
			</template>
			
			<template v-else>
				<block v-for="(item,index) in searchData" :key="index">
					<common-list :item="item" :index="index"></common-list>
				</block>
			</template>
		</view>
	</view>
</template>

<script>
	const mode = [{
			username: "乐视挂b", //用户名名称
			userpic: "/static/demo/topicpic/10.jpeg", //用户头像
			newstime: "2019-07-01 下午 4:22", //发布时间
			isFollow: false, //是否关注
			title: "我是标题", //标题
			titlepic: "/static/demo/datapic/11.jpg", //标题图片
			support: {
				type: "", //支持状态（顶、踩）
				support_count: 0, //顶 人数
				unsupport_count: 3 //踩  人数
			},
			comment_count: 2, //评论数
			share_num: 0 //分享数
		},
		{
			username: "呃釰宋", //用户名名称
			userpic: "/static/demo/topicpic/14.jpeg", //用户头像
			newstime: "2019-07-01 下午 4:22", //发布时间
			isFollow: false, //是否关注
			title: "我是标题", //标题
			titlepic: "", //标题图片
			support: {
				type: "", //支持状态（顶、踩）
				support_count: 1, //顶 人数
				unsupport_count: 3 //踩  人数
			},
			comment_count: 2, //评论数
			share_num: 0 //分享数
		},
		{
			username: "何之木木", //用户名名称
			userpic: "/static/demo/topicpic/12.jpeg", //用户头像
			newstime: "2019-07-01 下午 4:22", //发布时间
			isFollow: false, //是否关注
			title: "我是标题", //标题
			titlepic: "/static/demo/datapic/12.jpg", //标题图片
			support: {
				type: "", //支持状态（顶、踩）
				support_count: 0, //顶 人数
				unsupport_count: 0 //踩  人数
			},
			comment_count: 0, //评论数
			share_num: 0 //分享数
		}
	]
	
	import commonList from "@/components/common/common-list.vue"
	export default {
		components:{
			commonList
		},
		data() {
			return {
				searchText:'',
				list:['薇尔莉特紫罗兰永恒花园','你的名字','千与千寻','新海诚'],
				searchData:[]
			}
		},
		methods: {
			/* 点击搜索历史 */
			clickSearchHistory(text) {
				this.searchText = text
				this.searchEvent()
			},
			
			/* 搜索事件 */
			searchEvent(){
				uni.showLoading({
					title: '搜索中',
					mask: true
				})
				
				//模拟数据请求
				setTimeout(() => {
					uni.hideKeyboard()
					this.searchData = mode
					uni.hideLoading()
				},3000)
				
				console.log(this.searchText)
			},
		},
		
		/* 简单页面搜索输入 */
		onNavigationBarSearchInputChanged(e) {
			this.searchText = e.text
		},
		
		/* 监听点击原生搜索 */
		onNavigationBarButtonTap(e) {
			if(e.index === 0) {
				this.searchEvent()
			}
		},
	}
</script>

<style>

</style>
