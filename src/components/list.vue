<template>
	<view class="shop-box">
		<view class="shop" v-for="(r,i) in list" :key="i">
			<view class="shop-left" @click="choose(r)">
				<text style="color: #333333;font-size: 30upx;font-weight: bold;">{{r.name}}）</text>
				<view class="clo2">
					<text>
						{{r.distance}}
					</text>
					<text class="clo2-text2">
						{{r.address}}
					</text>
				</view>
				<text>
					营业时间：{{r.time}}
				</text>
				<text style="color: #E71563;">
					联系商家: {{r.tel}}
				</text>
				<text class="col-last" style="color: #FFA239;">
					自提
				</text>
			</view>
			<view class="shop-right" @click="go(r)">
				去下单
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			list: Array
		},
		data() {
			return {

			}
		},
		methods: {
			choose(r){
				let params = {
					long:r.long,
					lat: r.lat
				}
				this.$emit('getLocation',params)
			},
			go(r){
				let data = {
					name:r.name,
					distance:r.distance,
					address:r.address
				};
				uni.$emit('getShopParams',data);
				uni.switchTab({
					url:"../order/order"
				});
			}
		}
	}
</script>

<style>
	.shop-box{
		margin: 0 30upx;
	}
	.shop {
		box-sizing: border-box;
		padding: 20upx;
		border-radius: 20upx;
		border: 2px solid #DFDFDF;
		display: flex;
		align-items: center;
		margin-bottom: 15upx;
	}

	.shop .shop-left {
		flex: 1;
		display: flex;
		flex-direction: column;
	}

	.shop .shop-left text {
		font-size: 26upx;
		color: #666666;
		margin-bottom: 8upx;
	}

	.shop .shop-right {
		width: 160upx;
		display: flex;
		justify-content: center;
		align-items: center;
		color: #F280AA;
		font-size: 32upx;
	}

	.clo2 {
		box-sizing: border-box;
		display: flex;
		align-items: center;
		padding: 10upx 0;

	}

	.clo2-text2 {
		flex: 1;
		padding-left: 14upx;
		margin-left: 14upx;
		border-left: 1px solid #DFDFDF;
	}

	.col-last {
		width: 70upx;
		text-align: center;
		background-color: #FEF4E7;
		border: 1px solid #FFD5A7;
	}
</style>
