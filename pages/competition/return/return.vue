<template>
	<view class="competition">
		<image class="bg"
		src="https://s2.loli.net/2022/06/27/F2TViyH7ucsLA6D.png"></image>
		<view class="zsjd">
			<image 
		src="https://s2.loli.net/2022/06/27/7vUSrQdb2oHK6nh.png" ></image>
		</view>
		<view class="bin">
			<image class="bin1" @click="bin1"
		src="https://s2.loli.net/2022/06/27/FmfSrJiIO9hakqs.png" ></image>
		<image class="bin2" @click="bin2"
		src="https://s2.loli.net/2022/06/27/Uiog2nXFH7Iw8bd.png" ></image>
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
	
.competition{
	width: 100%;
	height: 808px;
	font-size: 40rpx;
	position: relative;
	
}
.bg{
	width: 100%;
	height:100%;
	margin-left: 0;
}

.zsjd{
	width: 60%;
	height: 150px;
	padding-top: 20px;
	position: absolute;
	/* margin: 0 auto; */
	left: 20%;
	top: 25%;
}
	
.zsjd image {
	width: 100%;
	height: 150px;
}
.bin {
	width: 100%;
	height: 65px;
	position: absolute;
	top: 50%;
	
}
.bin1 {
	float: left;
	width: 100px;
	height: 65px;
	margin-left: 20%;
}
.bin2 {
	float: left;
	width: 100px;
	height: 65px;
	margin-left: 10%;
}
</style>
