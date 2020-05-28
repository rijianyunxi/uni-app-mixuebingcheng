<template>
	<view class="login" @click="appLogin">
		<image class="img" :src="img"></image>
		<view class="msg">
			<text style="font-weight: bold;color: #FFFFFF;font-size: 35upx;padding-bottom: 10upx;">{{msg}}</text>
			<text>{{openId}}</text>
		</view>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				msg:'请登陆',
				openId:'',
				img:''
			}
		},
		methods:{
			appLogin(){
				if(!this.img){
					var that = this;
					uni.getProvider({
						service: 'oauth',
						success: function(res) {
							//console.log(res.provider);
							//支持微信、qq和微博等
							if (~res.provider.indexOf('weixin')) {
								uni.login({
									provider: 'weixin',
									success: function(loginRes) {
										console.log(loginRes);
										that._data.openId = loginRes.code;
										// 获取用户信息
										uni.getUserInfo({
											provider: 'weixin',
											success: function(infoRes) {
												that._data.msg = infoRes.userInfo.nickName;
												that._data.img = infoRes.userInfo.avatarUrl;
												console.log(infoRes.userInfo);
											}
										});
									}
								});
							}
						}
					});
				}
			},
		}
	}
</script>

<style scoped>
	.login{
		background-color: #E71563;
		color: #999999;
		display: flex;
		justify-content: center;
		align-items: center;
		font-size: 28upx;
		padding: 14upx;
	}
	.img{
		height: 140upx;
		width: 140upx;
	}
	.msg{
		flex:1;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: flex-start;
		padding-left: 14upx;
	}
</style>

