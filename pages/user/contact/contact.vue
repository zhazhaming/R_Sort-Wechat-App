<template>
	<view class="contact">
		
		<image class="bg"
		src="https://s2.loli.net/2022/06/27/hSwtpKcXf3Ze1sY.png"></image>
		<view class="our">
			<text>在使用小程序过程中，如果您有任何需求或建议，欢迎您进行反馈和建议！</text>
			<br>
			<br>
			<text>邮箱：xxxxxxxx@qq.com(测试)</text>
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
	font-size: 40rpx;
	position: relative;
	
}
.bg{
	width: 100%;
	height: 808px;
	margin-left: 0;
}

.our{
	width: 80%;
	
	line-height: 80rpx;
	position: absolute;
	/* margin: 0 auto; */
	left: 10%;
	top: 25%;
	color: rgb(137, 141, 144);
}
	


</style>
