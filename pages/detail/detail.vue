<template>
	<view>
		<!-- 帖子详细信息 -->
		<common-list :item='info' isDetail @doComment='doComment' @doShare='doShare' @follow='follow' @doSupport='doSupport'>
			特征实际就是
			<image :src="info.titlepic" mode=""></image>
			<image :src="info.titlepic" mode=""></image>
			<image :src="info.titlepic" mode=""></image>
			213w
		</common-list>

		<divider></divider>
		<!-- 评论 -->
		<view class="font-md font-weight-bold px-2 py-3">最新评论 3</view>
		<view class="px-2">
			<view class="flex align-start">
				<image src="../../static/demo/userpic/1.jpg" class="rounded-circle" style="height: 80rpx;width: 80rpx;"></image>
				<view class="flex flex-column flex-1 pl-2">
					<view class="font text-hover-primary">12312312</view>
					<view class="font-md ">123</view>
					<view class="font text-secondary">123123</view>
				</view>
			</view>
		</view>

		<!-- 弹出层 -->
		<moer-share ref='share'></moer-share>

		<!-- 占位 -->
		<view style="height: 100rpx;"></view>
		<bottom-input @submit='submit'></bottom-input>
	</view>
</template>

<script>
	import commonList from '@/components/common/common-list.vue'
	import bottomInput from '@/components/common/bottom-input.vue';
	import moerShare from '@/components/common/moer-share.vue';
	export default {
		components: {
			commonList,
			bottomInput,
			moerShare
		},
		data() {
			return {
				info: ''
			}
		},
		onLoad(e) {
			//初始化
			if (e.detail) this.__init(JSON.parse(e.detail))
		},
		methods: {
			//初始化
			__init(data) {
				//修改标题
				uni.setNavigationBarTitle({
					title: data.title
				})
				//请求api
				this.info = data
			},

			//点击关注
			follow() {
				this.info.isFollow = true
				uni.showToast({
					title: '关注成功'
				})
			},
			//顶踩功能
			doSupport(e) {
				const _info = this.info
				//相同操作，则终止掉
				if (_info.support.type === e.type) return false;
				//之前没有操作过
				if (_info.support.type === '') {
					_info.support[e.type + '_count']++
				} else if (_info.support.type === 'support' && e.type === 'unsupport') {
					_info.support.support_count--
					_info.support.unsupport_count++
				} else if (_info.support.type === 'unsupport' && e.type === 'support') {
					_info.support.support_count++
					_info.support.unsupport_count--
				}
				_info.support.type = e.type
			},
			//点击评论
			doComment() {
				console.log('评论')
			},
			//点击分享
			doShare() {
				console.log('点击分享')
			},
			//评论
			submit(data) {
				console.log(data)
			}
		},
		//监听原生导航
		onNavigationBarButtonTap() {
			this.$refs.share.open()
		},
		//返回按钮关闭弹出层
		onBackPress() {
			this.$refs.share.close()
		},
	}
</script>

<style>

</style>
