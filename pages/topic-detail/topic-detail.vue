<template>
	<view>
		<topic-info :info="info"></topic-info>
		<divider></divider>
		
		<view class="p-2 flex align-center border-bottom"
		hover-class="bg-light"
		 v-for="(item,index) in hotList" :key="index">
			<text class="iconfont icon-faxian text-main"></text>
			<view class="font text-dark text-ellipsis">
				{{item.title}}
			</view>
		</view>
		<divider></divider>
		
		<!-- tab -->
		<view class="flex align-center py-2">
			<view class="flex-1 flex-center  "
			v-for="(item,index) in tabBar" :key='index'
			:class="index === tabIndex ? 'font-lg text-main font-weight-bold' : 'font-md'"
			@click="change(index)">{{item.name}}</view>
		</view>
		<!-- 列表 -->
		<template v-if="listData.length > 0">
		<block v-for="(item,index) in listData" :key="index">
			<common-list :index='index' :item='item'></common-list>
			<divider></divider>
		</block>
		</template>
		<template v-else>
			<no-thing></no-thing>
		</template>
		<load-more :loadmore = 'loadText'></load-more>
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
	
	import topicInfo from '@/components/topic-detail/topic-info.vue';
	import commonList from '@/components/common/common-list.vue';
	import noThing from '@/components/common/no-thing.vue';
	import loadMore from '@/components/common/load-more.vue';
	export default {
		components:{
			topicInfo,
			commonList,
			noThing,
			loadMore
		},
		data() {
			return {
				info:{},
				hotList:[{
					title:"【新人必读】uni-app实在第二季商城类app开发(全栈)"
				},{
					title:"【升职必读】uni-app实在第三季模仿微信app开发(全栈)"
				}],
				tabIndex:0,
				tabBar:[{
					name:'默认'
				},{
					name:'最新'
				}],
				
				list1: [],
				loadText1:'上拉加载更多',
				
				list2:[],
				loadText2:'上拉加载更多',
			}
		},
		onLoad(option) {
			this.info = option.detail && JSON.parse(option.detail)
		
			this.list1 = mode
		},
		onReachBottom() {
			this.loadMore()
		},
		methods: {
			//导航点击
			change(index) {
				this.tabIndex = index
			},
			
			/* 上拉加载 */
			loadMore(){
				//拿到当前列表
				const index = this.tabIndex
				
				//判断当前列表是否可加载
				if(this.loadText !== '上拉加载更多') return false
				
				//设置当前页面的状态为加载中
				this['loadText'+(index+1)] = '加载中...'
				
				//模拟请求
				setTimeout(() => {
					this['list'+(index+1)] = [...this['list'+(index+1)],...this['list'+(index+1)]]
					this['loadText'+(index+1)] = '上拉加载更多'
				},3000)
			}
		},
		computed:{
			listData() {
				if(this.tabIndex === 0) {
					return this.list1
				}
				return this.list2
			},
			
			loadText() {
				return this['loadText'+(this.tabIndex+1)]
			}
		}
	}
</script>

<style>
.filter{
	filter: blur(10px);
}
</style>
