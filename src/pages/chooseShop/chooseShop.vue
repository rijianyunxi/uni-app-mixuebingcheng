<template>
	<view class="chooseShop">
		<view class="map_container">
			<map v-if="isShow" style="width: 100%; height: 500upx;" :latitude="latitude" :longitude="longitude" :scale="16"
			 :markers="covers">
			</map>
			<!-- <view @click="change">click me</view> -->
		</view>
		<view class="tab">
			<text class="tab-text">
				附近门店
			</text>
		</view>
		<scroll-view :scroll-y="true" class="scroll-list">
			<Shop :list="shopDate" @getLocation="getLocation"/>
		</scroll-view>
	</view>
</template>

<script>
	import Shop from '../../components/list.vue'
	export default {
		components:{
			Shop
		},
		data() {
			return {
				id: 0, // 使用 marker点击事件 需要填写id
				latitude: 35.08778,
				longitude: 112.57238,
				covers: [],
				shopDate: [],
				isShow: false
			}
		},
		methods: {
			getLocation(data){
				console.log(data);
				this.longitude = data.long;
				this.latitude = data.lat
			}
		},
		onLoad() {
			uni.$once("shopList", (data) => {
				this.shopDate = data;
				let res = data.map(r => {
					return {
						width: 35,
						height: 35,
						latitude: r.lat,
						longitude: r.long,
						iconPath: '../../static/location.png',
						title: r.name
					}
				});
				console.log(res);
				this.covers = res;
				this.isShow = true;
			});
		}
	}
</script>

<style>
	/* .chooseShop{
		display: flex;
		flex-direction: column;
	} */
 .tab{
	height: 80upx;
	 width: 100%;
	 box-sizing: border-box;
	 padding: 0 40upx;
	 display: flex;
	 align-items: center;
 }
 .tab-text{
	 line-height: 40upx;
	 color: #333333;
	 font-weight: bold;
	 font-size: 30upx;
	 padding: 0 14upx;
	 border-left: 2px solid #E50155;
 }
.scroll-list{
	height: 600upx;
}
</style>
