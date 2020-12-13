<template>
	<view>
		<view class="flex align-center py-2" style="100rpx" id="editor">
			<view class="flex-1 text-center" v-for="(item,index) in tabBar" :key='index' :class="index == tabIndex?'font-md text-main font-weight-bold':'font'"
			 @click="changeTab(index)">
				{{item.text}}
				<text class="ml-2" v-if="item.num">{{item.num}}</text>
			</view>
		</view>

		<swiper :duration="150" :current="tabIndex" @change="swiperChange" :style="'height:'+ schoolH +'px;'">
			<swiper-item v-for="(item,index) in friendList" :key='index'>
				<scroll-view scroll-y="true" :style="'height:'+ schoolH +'px;'" @scrolltolower='loadmore(index)'>
					<view>

						<template v-if="item.list.length > 0">
							<block v-for="(friend,f_index) in item.list" :key='f_index'>
								<user-list :friend='friend' :index='f_index'></user-list>
							</block>
							<load-more v-if="item.list.length > 10" :loadmore='item.loadmore'></load-more>
						</template>
						<template v-else>
							<no-thing></no-thing>
						</template>
					</view>
				</scroll-view>
			</swiper-item>
		</swiper>
	</view>
</template>

<script>
	const demo = [{
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
	}, {
		avatar: "/static/demo/userpic/17.jpg",
		username: "维萨",
		sex: 2, //0 未知 ，1女 ，2男
		age: 23,
		isFollow: false
	}, {
		avatar: "/static/demo/userpic/17.jpg",
		username: "维萨",
		sex: 2, //0 未知 ，1女 ，2男
		age: 23,
		isFollow: false
	}, {
		avatar: "/static/demo/userpic/12.jpg",
		username: "维萨",
		sex: 2, //0 未知 ，1女 ，2男
		age: 23,
		isFollow: false
	}, {
		avatar: "/static/demo/userpic/17.jpg",
		username: "维萨",
		sex: 2, //0 未知 ，1女 ，2男
		age: 23,
		isFollow: false
	}, {
		avatar: "/static/demo/userpic/17.jpg",
		username: "维萨",
		sex: 2, //0 未知 ，1女 ，2男
		age: 23,
		isFollow: false
	}, {
		avatar: "/static/demo/userpic/17.jpg",
		username: "维萨",
		sex: 2, //0 未知 ，1女 ，2男
		age: 23,
		isFollow: false
	}, {
		avatar: "/static/demo/userpic/17.jpg",
		username: "维萨",
		sex: 2, //0 未知 ，1女 ，2男
		age: 23,
		isFollow: false
	}, {
		avatar: "/static/demo/userpic/17.jpg",
		username: "维萨",
		sex: 2, //0 未知 ，1女 ，2男
		age: 23,
		isFollow: false
	}, {
		avatar: "/static/demo/userpic/17.jpg",
		username: "维萨",
		sex: 2, //0 未知 ，1女 ，2男
		age: 23,
		isFollow: false
	}];


	import noThing from "@/components/common/no-thing.vue"
	import loadMore from '@/components/common/load-more.vue';
	import userList from '@/components/user-list/user-list.vue'
	export default {
		components: {
			noThing,
			loadMore,
			userList
		},
		data() {
			return {
				schoolH: 0,
				tabIndex: 1,
				tabBar: [{
					text: '互关',
					num: 0
				}, {
					text: '关注',
					num: 3
				}, {
					text: '粉丝',
					num: 5
				}],

				friendList: []
			}
		},
		onLoad() {
			//获取可使用高度
			this.$nextTick(function() {
				const query = uni.createSelectorQuery().in(this);
				query.select('#editor').boundingClientRect(data => {
					//使用可用页面减去 导航高度
					this.schoolH = uni.getSystemInfoSync().windowHeight - data.height
				}).exec();
			})

			//获取数据
			this.getData()

		},
		methods: {
			//设置数据
			getData() {
				let arr = []
				this.tabBar.forEach((item, index) => {
					const obj = {
						loadmore: '上拉加载更多',
						list: []
					}
					if (index !== 0) obj.list = demo
					arr.push(obj)
				})

				this.friendList = arr
			},

			//点击导航栏
			changeTab(index) {
				this.tabIndex = index
			},

			//轮播图滑动
			swiperChange(e) {
				this.tabIndex = e.detail.current
			},

			//上拉事件
			loadmore(index) {
				var _item = this.friendList[index]
				if (_item.loadmore === '加载中...') return false

				_item.loadmore = '加载中...'
				setTimeout(() => {
					_item.loadmore = '上拉加载更多'
				}, 3000)
			}

		},
		//监听点击输入框事件
		onNavigationBarSearchInputClicked() {
			uni.navigateTo({
				url: "/pages/search/search"
			})
		},
		//监听点击取消
		onNavigationBarButtonTap() {
			uni.navigateBack({})
		}
	}
</script>

<style>

</style>
