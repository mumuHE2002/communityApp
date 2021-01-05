<template>
	<view>
		<view class="py-2 px-5 flex justify-around">
			<block v-for="(item,index) in providerList" :key='index'>
				<view :class="item.bgColor + ' '+ item.icon" class="text-white  font-lg rounded-circle flex-center" 
				style="width: 100rpx;height: 100rpx;" @click="login(item)"></view>
			</block>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				providerList: []
			}
		},
		mounted() {
			uni.getProvider({
				service: 'oauth',
				success: (result) => {
					this.providerList = result.provider.map((value) => {
						let providerName = '';
						let icon = ''
						let bgColor = ''
						switch (value) {
							case 'weixin':
								providerName = '微信登录'
								icon = 'iconfont icon-weixin'
								bgColor = 'bg-success'
								break;
							case 'qq':
								providerName = 'QQ登录'
								icon = 'iconfont icon-QQ'
								bgColor = 'bg-primary'
								break;
							case 'sinaweibo':
								providerName = '新浪微博登录'
								icon = 'iconfont icon-xinlangweibo'
								bgColor = 'bg-hover-danger'
								break;
						}
						return {
							name: providerName,
							id: value,
							icon,
							bgColor
						}
					});

				},
				fail: (error) => {
					console.log('获取登录通道失败', error);
				}
			});
		},
		methods:{
			login(item) {
				uni.login({
					provider:item.id,
					success: res => {
						//获取用户信息
						uni.getUserInfo({
							provider:item.id,
							success:infoRes => {
								let boj = {
									provider:item.id,
									openid:infoRes.userInfo.openId,
									expires_in:0,
									nickName:infoRes.userInfo.nickName,
									avatarUrl:infoRes.userInfo.avatarUrl
								}
								console.log(boj)
							}
						})
					},
					fail: res => {
						uni.showToast({
							title:'登录失败',
							icon:'none'
						})
					}
				})
			}
		}
	}
</script>

<style>
</style>
