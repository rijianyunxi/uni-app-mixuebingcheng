<template>
	<view class="order" @click="test()">
		order
	</view>
</template>

<script>
	export default {
		data() {
			return {

			}
		},
		methods: {
			test() {
				uni.chooseImage({
					count: 6,
					sizeType: ['original', 'compressed'],
					sourceType: ['album'],
					success: function(res) {
						// 预览图片
						uni.previewImage({
							urls: res.tempFilePaths,
							longPressActions: {
								itemList: ['发送给朋友', '保存图片', '收藏'],
								success: function(data) {
									console.log('选中了第' + (data.tapIndex + 1) + '个按钮,第' + (data.index + 1) + '张图片');
								},
								fail: function(err) {
									console.log(err.errMsg);
								}
							}
						});
					}
				});
			}
		},
		onLoad() {

		}
	}
</script>

<style>
	.order {
		height: 160upx;
		width: 100%;
		background-color: #007AFF;
	}
</style>
