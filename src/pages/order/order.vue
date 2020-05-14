<template>
	<view class="order-top">
		<view class="address" @click="chooseShop">
			<text style="color:#333333;font-size: 17px;font-weight: bold;">{{name}}</text>
			<view class="address-bottom">
				<text style="color: #FEB539;padding-right: 10upx;">约{{distance}}</text>
				<text>{{address}}</text>
			</view>
		</view>
		<view class="check">
			<view :class="[wayStatus ? 'bgactive' : 'unbgactive','bg']"></view>
			<view :class="['checked',wayStatus ? 'textactive' : '']" @click="chooseWays">到店</view>
			<view :class="['checked',wayStatus ? '' : 'textactive']" @click="chooseWays">外卖</view>
		</view>
	</view>
</template>

<script>
	import list from '../../static/shop.js'
	export default {
		data() {
			return {
				wayStatus: true,
				name:"蜜雪冰城（大张店)",
				distance:"3.8km",
				address:"信尧广场大张盛德美购物广场出口南门第一家"
			}
		},
		methods: {
			chooseShop() {
				setTimeout(() => {
					uni.$emit("shopList", list);
				}, 500);
				uni.navigateTo({
					url: "../chooseShop/chooseShop"
				});
			},
			chooseWays(){
				this.wayStatus = !this.wayStatus
			}
		},
		onLoad() {
			uni.$once('getShopParams',(data)=>{
				this.name = data.name;
				this.distance = data.distance;
				this.address = data.address
			})
		}
	}
</script>

<style>
	.order-top{
		box-sizing: border-box;
		height: 150upx;
		display: flex;
		justify-content: center;
		align-items: center;
		padding: 0 20upx;
		border-bottom: 1px solid #ECECEC;
	}
	.address{
		flex:1;
		display: flex;
		flex-direction: column;
		color: #9E9E9E;
		font-size: 24upx;
	}
	.check{
		width: 140upx;
		height: 60upx;
		border-radius: 35upx;
		border: 1px solid #E50155;
		display: flex;
		align-items: center;
		overflow: hidden;
		position: relative;
	}
	.check .bg{
		height: 50upx;
		width: 70upx;
		border-radius: 25upx;
		background: #E50155;
		position: absolute;
		/* left: 5upx; */
		top: 5upx;
	}
	.bgactive{
		left: 5upx;
	}
	.unbgactive{
		right: 5upx;
	}
	.check .checked{
		flex:1;
		height: 60upx;
		line-height: 60upx;
		text-align: center;
		/* color: #9E9E9E; */
		font-size: 24upx;
		z-index: 10;
	}
	.textactive{
		color: #FFFFFF;
	}
</style>
