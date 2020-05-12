<template>
	<view class="content">
		<!-- 轮播图开始 -->
		<swiper class="swiper-box" :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
			<swiper-item v-for="(r,i) in swiper" :key="i">
				<image style="width: 100%; height: 380upx;" :src="r" mode="aspectFill"></image>
			</swiper-item>
		</swiper>
		<!-- 轮播图结束 -->
		<!-- 列表开始 -->
		<view class="list-box">
			<view class="list" v-for="(r,i) in list" :key="i" @click="go(i)">
				<view class="list-icon">
					<image style="height: 50upx;width: 70upx;" :src="r.srcLeft" mode=""></image>
				</view>
				<view class="list-text">
					<text style="color: #4D4D4D;font-size: 34upx;font-weight: bold;">{{r.textTop}}</text>
					<text>{{r.textBottom}}</text>
				</view>
				<view>
					<image style="height: 30upx;width: 30upx;" :src="r.srcRight" mode=""></image>
				</view>
			</view>
		</view>
		<!-- 列表结束 -->
		<!-- 底部图片 -->
		<view class="bottom">
			<image style="height: 200upx;width: 100%;" src="../../static/bottom-img.png" mode=""></image>
		</view>
		<!-- 结束 -->
	</view>
</template>

<script>
	export default {
		data() {
			return {
				swiper: [
					"http://img4.imgtn.bdimg.com/it/u=766451773,569360703&fm=26&gp=0.jpg",
					"http://img.91jm.com/2016/05/4RAXIc1NcXt5.jpg",
					"http://img0.imgtn.bdimg.com/it/u=1631218320,1235924202&fm=26&gp=0.jpg"
				],
				list:[
					{
						srcLeft:"../../static/icon-list/shoujidiancan.png",
						textTop:"手机点餐",
						textBottom:"无需排队，快速下单",
						srcRight:"../../static/icon-list/you.png",
					},
					{
						srcLeft:"../../static/icon-list/duihuanma.png",
						textTop:"兑换码",
						textBottom:"输入兑换码，兑换优惠券",
						srcRight:"../../static/icon-list/you.png",
					},
					{
						srcLeft:"../../static/icon-list/youhuiquan.png",
						textTop:"优惠券",
						textBottom:"下单优惠，纵享甜蜜",
						srcRight:"../../static/icon-list/you.png",
					}
				]
			}
		},
		methods: {
			go(index){
				if(index===0){
					uni.switchTab({
					         url: '../order/order'
					});
				}else{
					uni.navigateTo({
					       url: '../youhuiquan/youhuiquan'
					});
				}
			}
		}
	}
</script>

<style>
	.swiper-box {
		height: 380upx;
		width: 100%;
	}
	.list-box{
		width: 100%;
		box-sizing: border-box;
		padding: 0 5%;
	}
	.list-box .list{
		height: 200upx;
		width: 100%;
		box-sizing: border-box;
		display: flex;
		align-items: center;
		border-bottom: 1px solid #F1F1F1;
	}
	.list-box .list-text{
		display: flex;
		flex-direction: column;
		flex: 1;
		color: #7B7B7B;
		font-size: 26upx;
		box-sizing: border-box;
	}
	.list-box .list-icon{
		height: 100upx;
		width: 100upx;
		background: #FFF2DF;
		border-radius: 50%;
		display: flex;
		justify-content: center;
		align-items: center;
		margin-right: 20upx;
	}
	.bottom{
		box-sizing: border-box;
		width: 90%;
		height:200upx;
		border-radius: 15upx;
		margin-left: 5%;
		margin-top: 50upx;
		overflow: hidden;
	}
</style>
