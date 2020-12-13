<template>
<view>
	<view @click="wds" class="py-2 mx-2 flex align-center border-bottom border-light-secondary " hover-class="bg-light">
		<image :src="item.avatar" class="rounded-circle mr-2" style="width: 100rpx;height: 100rpx;"></image>
		<view class="flex flex-column flex-1">
			<text class="font-md text-dark">{{item.username}}</text>
			<uni-badge v-if="item.sex" :text="item.age" :type="item.sex === 1 ? 'error' : 'primary' " size="small">
				<text class="iconfont  text-white " :class="item.sex === 1?'icon-nv':'icon-nan'" style="font-size: 12px; margin-right: 5rpx;"></text>
			</uni-badge>
		</view>
		<view class="uni-icon uni-icon-checkbox-filled ml-auto " :class="item.isFollow ? 'text-light-muted' : 'text-main'"></view>
	</view>
</view>
</template>

<script>
	import uniBadge from '@/components/uni-components/uni-badge/uni-badge.vue'
	export default {
		props: {
			item: Object,
			index: Number
		},
		components: {
			uniBadge
		},
		methods:{
			wds() {
				console.log(this.index)
			}
		}
	}
</script>

<style>
</style>
