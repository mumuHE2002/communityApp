<template>
	<view>
		<uni-list-item title="头像" link @click="changeUserpic">
			<image :src="userpic" slot='footer'
			style="width: 100rpx; height: 100rpx;" class="rounded-circle"></image>
			<text slot='right-icon' class="iconfont icon-bianji1 uni-icon-wrapper" ></text>
		</uni-list-item>
		<uni-list-item title="昵称" link>
			<input type="text" slot='footer' v-model="uname" />
			<text slot='right-icon' class="iconfont icon-bianji1 uni-icon-wrapper" ></text>
		</uni-list-item>
		<uni-list-item title="性别" link @click="changeSex">
			<view slot='footer'>{{sexText}}</view>
			<text slot='right-icon' class="iconfont icon-bianji1 uni-icon-wrapper" ></text>
		</uni-list-item>

			<uni-list-item title="生日" link>
				<picker mode="date" :value="birthday" @change="onDateChange" slot='footer' >
					<view >{{birthday}}</view>
				</picker>
				<text slot='right-icon' class="iconfont icon-bianji1 uni-icon-wrapper" ></text>
			</uni-list-item>

		<uni-list-item title="感情" link @click="changeEmotion">
			<view slot='footer'>{{emotionText}}</view>
			<text slot='right-icon' class="iconfont icon-bianji1 uni-icon-wrapper" ></text>
		</uni-list-item>
		<uni-list-item title="职业" link @click="changeJob">
			<view slot='footer'>{{job}}</view>
			<text slot='right-icon' class="iconfont icon-bianji1 uni-icon-wrapper" ></text>
		</uni-list-item>
		<uni-list-item title="家乡" link @click="showCity">
			<view slot='footer'>{{pickerText}}</view>
			<text slot='right-icon' class="iconfont icon-bianji1 uni-icon-wrapper" ></text>
		</uni-list-item>
		
		<view class="p-2">
			<button class="bg-main text-white " style="border-radius: 50px;">完成</button>
		</view>
		
		<mpvue-city-picker :themeColor="themeColor" ref='mpvure' :pickerValueDefault="pickerValueDefault"
		 @onConfirm='onConfirm'></mpvue-city-picker>
	</view>
</template>

<script>
	const sexArr = ['保密','男','女']
	const emotionArr = ['保密','未婚','已婚']
	const jobArr = ['程序员','教师','银行','船夫','打工人','干饭人']
	import uniListItem from '@/components/uni-components/uni-list-item/uni-list-item.vue'
	import mpvueCityPicker from '@/components/uni-components/mpvue-citypicker/mpvueCityPicker.vue';
	export default {
		components:{
			uniListItem,
			mpvueCityPicker
		},
		data() {
			return {
				themeColor:'',
				pickerValueDefault:[0,0,1],
				pickerText:'',
				
				
				userpic:'/static/demo/userpic/1.jpg',
				uname:'昵称',
				sex:0,
				emotion:0,
				job:'不告诉你',
				birthday:"2020-12-23",
				
			}
		},
		methods: {
			/* uniapp 官方三级联动 */
			onConfirm(e) {
				this.pickerText = e.label
				console.log(this.pickerText)
			},
			
			showCity() {
				this.$refs.mpvure.show()
			},
			
			/* 修改头像 */
			changeUserpic() {
				uni.chooseImage({
					count:1,
					sizeType:['compressed']
				}).then(res => {
					res = res[1]
					this.userpic = res.tempFilePaths[0]
				})
			},
			
			/* 修改性别 */
			changeSex() {
				uni.showActionSheet({
				    itemList: sexArr,
				    success: (res) =>  {
				        this.sex = res.tapIndex
				    },
				   
				});
			},
			
			/* 修改情感 */
			changeEmotion() {
				uni.showActionSheet({
					itemList:emotionArr,
					success: (res) => {
						this.emotion = res.tapIndex
					}
				})
			},
			
			/* 修改生日 */
			onDateChange(e) {
				this.birthday = e.detail.value
			},
			
			/* 修改职业 */
			changeJob() {
				uni.showActionSheet({
					itemList:jobArr,
					success: (res) => {
						this.job = jobArr[res.tapIndex]
					}
				})
			}
			
			
		},
		computed:{
			sexText() {
				return sexArr[this.sex]
			},
			emotionText() {
				return emotionArr[this.emotion]
			},
		},
		onBackPress() {
			if(this.$refs.mpvure.showPicker) {
				this.$refs.mpvure.pickerCancel()
			}
		},
		onUnload() {
			if(this.$refs.mpvure.showPicker) {
				this.$refs.mpvure.pickerCancel()
			}
		}
	}
</script>

<style>
	.uni-icon-wrapper {
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		align-items: center;
		padding: 0 10px;
	}
	input {
		text-align: right;
	}
</style>
