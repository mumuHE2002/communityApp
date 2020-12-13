<template>
	<view>
		<view class="">

			<template v-if="searchData.length === 0">
				<view class="font-md mx-2">
					搜索历史
				</view>
				<view class="flex flex-wrap">
					<view class="border rounded px-2 mx-2 my-1 " v-for="(item,index) in list" :key="index" hover-class="bg-light"
					 @click="clickSearchHistory(item)">{{item}}</view>
				</view>
			</template>

			<template v-else>
				<block v-for="(item,index) in searchData" :key="index">
					<template v-if="type === 'post'">
						<!-- 帖子 -->
						<common-list :item="item" :index="index"></common-list>
					</template>
					<template v-else-if="type === 'topic'">
						<!-- 话题 -->
						<topic-list :item="item" :index="index"></topic-list>
					</template>
					<template v-else-if="type === 'user'">
						<!-- 用户 -->
						<user-list :item="item" :index="index"></user-list>
					</template>
				</block>
			</template>
		</view>
	</view>
</template>

<script>
	const postDemo = [{
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

	const topicDemo = [{
		cover: "/static/demo/topicpic/1.jpeg",
		title: "话题标题2333",
		desc: "我是描述",
		today_count: 0,
		news_count: 0
	}, {
		cover: "/static/demo/topicpic/1.jpeg",
		title: "话题标题2333",
		desc: "我是描述",
		today_count: 0,
		news_count: 0
	}, {
		cover: "/static/demo/topicpic/1.jpeg",
		title: "话题标题2333",
		desc: "我是描述",
		today_count: 0,
		news_count: 0
	}, {
		cover: "/static/demo/topicpic/1.jpeg",
		title: "话题标题2333",
		desc: "我是描述",
		today_count: 0,
		news_count: 0
	}, {
		cover: "/static/demo/topicpic/1.jpeg",
		title: "话题标题2333",
		desc: "我是描述",
		today_count: 0,
		news_count: 0
	}];

	const userDemo = [{
		avatar: "/static/demo/userpic/16.jpg",
		username: "木木一只",
		sex: 1, //0 未知 ，1女 ，2男
		age: 23,
		isFollow: true
	}, {
		avatar: "/static/demo/userpic/17.jpg",
		username: "维萨",
		sex: 2, //0 未知 ，1女 ，2男
		age: 23,
		isFollow: false
	}, {
		avatar: "/static/demo/userpic/18.jpg",
		username: "维萨",
		sex: 2, //0 未知 ，1女 ，2男
		age: 23,
		isFollow: false
	}];

	import commonList from "@/components/common/common-list.vue"
	import topicList from '@/components/news/topic-list.vue'
	import userList from '@/components/user-list/user-list.vue'
	export default {
		components: {
			commonList,
			topicList,
			userList
		},
		data() {
			return {
				searchText: '',
				list: ['薇尔莉特紫罗兰永恒花园', '你的名字', '千与千寻', '新海诚'],
				searchData: [],

				//当前的搜索类型
				type: "post"
			}
		},
		onLoad(e) {
			if (e.type) this.type = e.type

			let pageTitle = '帖子'
			switch (this.type) {
				case 'post':
					pageTitle = '帖子'
					break
				case 'topic':
					pageTitle = '话题'
					break
				case 'user':
					pageTitle = '用户'
					break
			}

			//修改搜索占位
			// #ifdef APP-PLUS
			//获取当前窗口对象实例
			let currentWebview = this.$mp.page.$getAppWebview()
			//获取当前窗口原生导航栏
			let th = currentWebview.getStyle().titleNView
			//修改当前窗口搜索框里的数据
			th.searchInput.placeholder = '搜索' + pageTitle
			//重写原生导航
			currentWebview.setStyle({
				titleNView: th
			})
			// #endif


		},
		methods: {
			/* 点击搜索历史 */
			clickSearchHistory(text) {
				this.searchText = text
				this.searchEvent()
			},

			/* 搜索事件 */
			searchEvent() {
				uni.showLoading({
					title: '搜索中',
					mask: true
				})

				//模拟数据请求
				setTimeout(() => {
					switch (this.type) {
						case 'post':
							this.searchData = postDemo
							break
						case 'topic':
							this.searchData = topicDemo
							break
						case 'user':
							this.searchData = userDemo
							break
					}
					uni.hideKeyboard()

					uni.hideLoading()
				}, 3000)

				console.log(this.searchText)
			},
		},

		/* 简单页面搜索输入 */
		onNavigationBarSearchInputChanged(e) {
			this.searchText = e.text
		},

		/* 监听点击原生搜索 */
		onNavigationBarButtonTap(e) {
			if (e.index === 0) {
				this.searchEvent()
			}
		},
	}
</script>

<style>

</style>
