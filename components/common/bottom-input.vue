<template>
	<view id="a" class="fixed-bottom flex align-center border-top border-light bg-white" style="height: 100rpx;">
		<input class="flex-1 bg-light rounded ml-2 py-1 px-2 font" 
		type="text" placeholder="文明发言" v-model="content" @confirm='submit'/>
		<view class="iconfont icon-fabu font-lg flex-center animated" 
		hover-class="jello text-main" style="width: 100rpx;"
		@click="submit"></view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				content :''
			}
		},
		methods:{
			submit(){
				if(this.content !== '') {
					this.$emit('submit',this.content)
					this.content = ''
				}
			}
		}
	}
</script>

<style>
</style>
