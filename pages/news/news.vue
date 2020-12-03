<template>
	<view>
		<uni-nav-bar :border="false" :statusBar='true' @clickRight="openAddInput">
			<view class="flex-center font-weight-bold">
				<view v-for="(item,index) in navBar" :key="index"
				class="mx-1" :class="tabIndex == index?'font-lg text-main':'font-md text-light-muted'"
				@click="changeTab(index)" >
				{{item.text}}
				</view>
			</view>
			<text class="iconfont icon-fatie_icon font-lg" slot="right"></text>
		</uni-nav-bar>
		
		<swiper  :current="tabIndex" @change="onChange" :duration="150" :style="'height:' + scroolH + 'px;'" >
			<swiper-item>
				<scroll-view scroll-y="true" :style="'height:' + scroolH + 'px;'" @scrolltolower='onLoadmore'>
					<view>
						<block v-for="(item,index) in newsList" :key='index'>
							<common-list :item='item' :index='index' @doSupport="doSupport"></common-list>
							<divider></divider>
						</block>
						<load-more :loadmore='loadmore'></load-more>
					</view>
				</scroll-view>
			</swiper-item>
			<swiper-item>
				<scroll-view scroll-y="true" :style="'height:' + scroolH + 'px;'" >
					<view>
						<!-- 热门分类 -->
						<hot-cate :hotCate="hotCate" @openMore='openMore'></hot-cate>
						<!-- 搜索话题 -->
						<view class="p-2">
							<view class="flex-center bg-gray text-secondary py-2 rounded">
								<text class="iconfont icon-sousuo"></text>
								搜索话题
							</view>
						</view>
						<!-- 轮播图 -->
						<swiper class="px-2 pb-2" :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
						
							<swiper-item v-for="(item,index) in 4" :key='index'>
								<view class="rounded-md overflow-hidden" style="height: 300rpx;">
									<image style="width: 100%; height: 100%;" src="/static/demo/datapic/31.jpg" ></image>
								</view>
							</swiper-item>
						</swiper>
						<divider></divider>
						<!-- 最近更新 -->
						<view class="font-md px-2 py-3">最近更新</view>
						<block v-for="(item,index) in topicList" :key="index">
							<topic-list :item='item' :index='index' @openTopic='openTopic'></topic-list>
						</block>
					</view>
				</scroll-view>
			</swiper-item>
		</swiper>
	</view>
</template>

<script>
	const mode = [{
			username: "乐视挂b", //用户名名称
			userpic: "/static/demo/topicpic/10.jpeg", //用户头像
			newstime: "2019-07-01 下午 4:22", //发布时间
			isFollow: true, //是否关注
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
			isFollow: true, //是否关注
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
			isFollow: true, //是否关注
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
	import uniNavBar from '@/components/uni-components/uni-nav-bar/uni-nav-bar.vue'
	import commonList from '@/components/common/common-list.vue';
	import loadMore from '@/components/common/load-more.vue';
	import hotCate from '@/components/news/hot-cate.vue';
	import topicList from '@/components/news/topic-list.vue';
	export default {
		components:{
			uniNavBar,
			commonList,
			loadMore,
			hotCate,
			topicList
		},
		data() {
			return {
				scroolH:0,
				tabIndex:0,
				navBar:[{
					text:"关注"
				},{
					text:"话题"
				}],
				newsList:[],
				loadmore:"上拉加载更多",
				
				hotCate:[{
					name:"关注"
				},{
					name:"推荐"
				},{
					name:"体育"
				},{
					name:"热点"
				},{
					name:"财经"
				},{
					name:"娱乐"
				}],
				
				topicList:[{
					cover:"/static/demo/topicpic/1.jpeg",
					title:"话题标题2333",
					desc:"我是描述",
					today_count:0,
					news_count:0
				},{
					cover:"/static/demo/topicpic/1.jpeg",
					title:"话题标题2333",
					desc:"我是描述",
					today_count:0,
					news_count:0
				},{
					cover:"/static/demo/topicpic/1.jpeg",
					title:"话题标题2333",
					desc:"我是描述",
					today_count:0,
					news_count:0
				},{
					cover:"/static/demo/topicpic/1.jpeg",
					title:"话题标题2333",
					desc:"我是描述",
					today_count:0,
					news_count:0
				},{
					cover:"/static/demo/topicpic/1.jpeg",
					title:"话题标题2333",
					desc:"我是描述",
					today_count:0,
					news_count:0
				},]
			}
		},
		onLoad() {
			this.getSys()
			this.newsList = mode
		},
		methods: {
			/* 点击切换导航 */
			changeTab(index) {
				this.tabIndex = index
			},
			
			/* 获取scrool 可以使用的高度 */
			getSys(){
				const sys = uni.getSystemInfoSync()
				this.scroolH = sys.windowHeight - sys.statusBarHeight - 44
			},
			
			/* swiper 滑动事件 */
			onChange(e){
				this.tabIndex = e.detail.current
			},
			
			/* 顶踩操作 */
			doSupport(e) {
				const item = this.newsList[e.index]
			
				//如果没有状态，表示没有操作过，直接让当前操作 + 1
				if (item.support.type === "") {
					item.support[e.type + '_count']++
				} else if (item.support.type === "support" && e.type === "unsupport") {
					//如果状态值为 顶 而且用户点击了 踩
					//则让 顶 -1 ， 踩 +1
					item.support.support_count--
					item.support.unsupport_count++
				} else if (item.support.type === "unsupport" && e.type === "support") {
					//如果状态为 踩 而且用户点击了 顶
					//则让 踩 -1 顶 +1
					item.support.unsupport_count--
					item.support.support_count++
				}
				item.support.type = e.type
			},
			
			/* 上拉事件 */
			onLoadmore(){
				if(this.loadmore !== '上拉加载更多') return false
				
				this.loadmore = "加载中..."
				
				setTimeout(() => {
					this.newsList = [...this.newsList,...this.newsList]
					this.loadmore = "上拉加载更多"
				},3000)
				
			},
			
			/* 跳转页面 分类页面 */
			openMore() {
				console.log(123)
				uni.navigateTo({url:"/pages/topic-nav/topic-nav"})
			},
			
			/* 打开话题详情 */
			openTopic(e) {
				uni.navigateTo({url:"/pages/topic-detail/topic-detail?detail="+JSON.stringify(e)})
			},
			
			/* 打开发布页面 */
			openAddInput() {
				uni.navigateTo({url:'/pages/add-input/add-input'})
			}
		}
	}
</script>

<style>

</style>
