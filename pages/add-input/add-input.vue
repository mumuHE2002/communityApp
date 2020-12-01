<template>
	<view>
		<uni-nav-bar left-icon="back" statusBar :border="false" @clickLeft="navBack">
			<view>
			所有人可见
				<text class="iconfont icon-shezhi"></text>
			</view>
		</uni-nav-bar>
		
		<!-- 文本域 -->
		<textarea class="uni-textarea px-2" v-model="content" placeholder="说一句话吧"></textarea>
		
		<!-- 上传图片选择 -->
		<up-image :show="upImageIsShow" ref='uploadImage' @change='changeImage' :storeImg='imgList'></up-image>
		
		<!-- 底部 -->
		<view class="fixed-bottom flex align-center" style="height: 86rpx;">
			<view class="iconfont icon-caidan footer-btn animated"
			hover-class="jello"></view>
			<view class="iconfont icon-huati footer-btn animated"
			hover-class="jello" ></view>
			<view class="iconfont icon-tupian footer-btn animated"
			hover-class="jello" @click="iconClickEvent('uploadImage')" ></view>
			<view class="bg-main ml-auto text-white flex-center rounded mr-2 animated"
			 hover-class="jello" style="width: 140rpx;height: 60rpx;">发送</view>
		</view>
	</view>
</template>

<script>
	import uniNavBar from '@/components/uni-components/uni-nav-bar/uni-nav-bar.vue';
	import upImage from '@/components/common/up-image.vue'
	export default {
		components:{
			uniNavBar,
			upImage
		},
		data() {
			return {
				content:"",
				imgList:[],
				isBack:false
			}
		},

		methods: {
			/* 导航返回 */
			navBack(){
				uni.navigateBack({})
			},
			
			/* 底部按钮点击事件 */
			iconClickEvent(e) {
				switch (e){
					case 'uploadImage':
					this.$refs.uploadImage.chooseImage()
						break
				}
			},
			
			/* 图片列表 */
			changeImage(e) {
				this.imgList = e
			},
			
			/* 保存到本地 */
			store() {
				const data = {
					content:this.content,
					imgList:this.imgList
				}
				uni.setStorageSync('add_input',JSON.stringify(data))
			},
			
			/* 删除本地数据 */
			removeStore() {
				uni.removeStorageSync('add_input')
			},
			
			/* 页面加载数据 */
			getStore() {
				if(!uni.getStorageSync('add_input')) return false
				const data = JSON.parse(uni.getStorageSync('add_input'))
				this.imgList = data.imgList
				this.content = data.content
			}
		},
		computed:{
				upImageIsShow() {
					return this.imgList.length > 0
				}
		},
		onLoad() {
			this.getStore()
		},
		onBackPress() {
			if((this.content !== '' || this.imgList.length !== 0) && !this.isBack) {
				uni.showModal({
					content:"是否保存",
					cancelText:'不保存',
					confirmText:'保存',
					success: res => {
						if(res.confirm) {
							this.store()
						}
						if(res.cancel) {
							this.removeStore()
						}
						uni.navigateBack({})
					}
				})
				
				this.isBack = true
				return true
			}
		}
	}
</script>

<style>
.footer-btn{
	width: 86rpx;
	height: 86rpx;
	display: flex;
	justify-content: center;
	align-content: center;
	font-size: 50rpx;
}
</style>
