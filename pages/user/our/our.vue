<template>
	<view class="contact">
		
		<image class="bg"
		src="https://s2.loli.net/2022/06/27/hSwtpKcXf3Ze1sY.png"></image>
		<view class="our">
			<h1>R Sort</h1>
			<text>快速轻松帮您判断垃圾类别，只需要拍照就能识别是什么垃圾！</text>
			<br>
			
			<text>欢迎分享R Rort官方小程序</text><br>
			<text>点击二维码图片，即可保存！</text>
		</view>
		
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			bin1(){
				wx.navigateTo({
					url: `/pages/competition/competition`
				})
			},
			bin2(){
				wx.switchTab({
				            url: `/pages/index/index`
				})
			}
		}
	}
</script>

<style>
	
.contact{
	width: 100%;
	height: 808px;
	font-size: 35rpx;
	position: relative;
	
}
.bg{
	width: 100%;
	height: 808px;
	margin-left: 0;
}

.our{
	width: 80%;
	
	line-height: 70rpx;
	position: absolute;
	/* margin: 0 auto; */
	left: 10%;
	top: 5%;
	color: rgb(137, 141, 144);
}
h1{
	font-size: 70rpx;
	text-align: center;
}


</style>
