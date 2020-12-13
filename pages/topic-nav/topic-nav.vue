<template>
	<view>
		<scroll-view scroll-x class="scroll-row" :scroll-into-view="scrollInto" scroll-with-animation>
			<view>
				<view v-for="(item,index) in tabBars" class="scroll-row-item px-3 py-2 font-md " :id="'tab'+index" :class="tabIndex === index ? 'text-main font-lg font-weight-bold':''"
				 @click="changeItem(index)" style="height: 100rpx; box-sizing: border-box;">{{item.name}}</view>
			</view>
		</scroll-view>

		<swiper @tap.stop :duration="150" :current="tabIndex" @change="onChangeTab" :style="'height:'+scrollH+ 'px;'">
			<swiper-item v-for="(item,index) in newsList" :key="">
				
				<scroll-view scroll-y="true" :style="'height:'+scrollH+ 'px;'"  @scrolltolower="loadmore(index)">
					<view>
						<template v-if="item.list.length > 0">
							<block v-for="(item02,index02) in item.list" :key="index02">
								<topic-list :item="item02" :index="index02"></topic-list>
							</block>
						
							<!-- 上拉加载更多 -->
							<load-more :loadmore="item.loadmore"></load-more>
						</template>
						
						<template v-else>
							<!-- 什么都没有 -->
							<no-thing></no-thing>
						</template>
					</view>
				</scroll-view>
			</swiper-item>
		</swiper>

	</view>
</template>

<script>
	const mode = [{
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
				}];


	import topicList from '@/components/news/topic-list.vue'
	import loadMore from '@/components/common/load-more.vue';
	export default {
		components: {
			topicList,
			loadMore
		},
		data() {
			return {
				scrollH: 0,

				//顶部选项卡
				scrollInto: "",
				tabIndex: 0,
				tabBars: [{
					name: "关注"
				}, {
					name: "推荐"
				}, {
					name: "热点"
				}, {
					name: "财经"
				}, {
					name: "娱乐"
				}, {
					name: "军事"
				}, {
					name: "历史"
				}],
				newsList: []
			}
		},
		onLoad() {
			this.getSysH() //页面加载计算出滑动高度

			this.getData() //加载数据
		},
		methods: {

			/* 加载假数据 */
			getData() {
				let arr = []
				this.tabBars.forEach((item, index) => {
					const obj = {
						loadmore: "上拉加载更多",
						list: []
					}
					if (index < 2) {
						obj.list = mode
					}

					arr.push(obj)
				})
				this.newsList = arr
			},

			/* 关注按钮 */
			follow(e) {
				//获取到是那一页的列表
				const list = this.newsList[this.tabIndex].list
				list[e].isFollow = true
				uni.showToast({
					title: "关注成功"
				})
			},

			/* 点赞，踩操作 */
			doSupport(e) {
				const list = this.newsList[this.tabIndex].list
				const item = list[e.index]

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

			/* 
					切换导航分页
			 */
			changeItem(index) {
				if (this.tabIndex === index) {
					return false;
				}

				this.tabIndex = index
				this.scrollInto = "tab" + index
			},

			//滑动切换
			onChangeTab(e) {
				this.changeItem(e.detail.current)
			},

			//上拉加载更多
			loadmore(index) {
				const item = this.newsList[index]

				//获取加载状态
				if (item.loadmore !== "上拉加载更多") return

				//修改加载状态
				item.loadmore = "加载中..."

				//模拟加载请求
				setTimeout(() => {
					item.list = [...item.list, ...item.list]

					item.loadmore = "上拉加载更多"
				}, 2000)
			},

			//获取手机屏幕高度
			getSysH() {
				uni.getSystemInfo({
					success: res => {
						this.scrollH = res.windowHeight - 56
					}
				})
			}
		},
		onNavigationBarSearchInputClicked() {
			uni.navigateTo({
				url:"/pages/search/search"
			})
		},
		onNavigationBarButtonTap() {
			uni.navigateTo({
				url:"/pages/add-input/add-input"
			})
		},
	}
</script>

<style lang="less">

</style>
