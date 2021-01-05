<template>
	<view>
		<uni-collapse>
			<uni-collapse-item title="标题文字" showAnimation>
				<view>asdasd</view>
			</uni-collapse-item>
		</uni-collapse>
		
		<view class="p-2">
			<button class="bg-main text-white " style="border-radius: 50px;">意见反馈</button>
		</view>
		
	</view>
</template>

<script>
	import uniCollapse from '@/components/uni-components/uni-collapse/uni-collapse.vue';
	import uniCollapseItem from '@/components/uni-components/uni-collapse-item/uni-collapse-item.vue';
	export default {
		components:{
			uniCollapse,
			uniCollapseItem
		},
		data() {
			return {
				
			}
		},
		methods: {
			
		}
	}
</script>

<style>

</style>
