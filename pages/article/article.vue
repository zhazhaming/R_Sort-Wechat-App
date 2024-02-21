<template>
	<view class="page">
		<view class="bg">
			<image 
			src="https://picst.sunbangyan.cn/2024/01/27/3d77af362dcfd97a2a9ea8bcb9c9aad7.jpeg" 
			></image>
		</view>
		<view class="article1"  @click="art1">
			<image src="https://picdl.sunbangyan.cn/2024/01/27/32692de65df90a293b4b461d787051f8.jpeg" ></image>
			
		</view>
		<view class="article2" @click="art2">
			<image src="https://picdl.sunbangyan.cn/2024/01/27/b3805b85712e234479ccb8660cca4b16.jpeg" ></image>
		</view>
		<view class="article3" @click="art3">
			<image src="https://picss.sunbangyan.cn/2024/01/27/88b9cb5d68097468f9673a83c4bbbd3d.jpeg" ></image>
		</view>
		<view class="article4" @click="art4">
			<image src="https://picdm.sunbangyan.cn/2024/01/27/80271359c71333abd6ea80b7392a1589.jpeg" ></image>
		</view>
		<view class="article5" @click="art5">
			<image src="https://picss.sunbangyan.cn/2024/01/27/f7d64b4116940dafb7bef764c2c6ed76.jpeg" ></image>
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
			art1() {
				wx.navigateTo({
					url: './out1/out1'
				})
			},
			art2() {
				wx.navigateTo({
					url: './out2/out2'
				})
			},
			art3() {
				wx.navigateTo({
					url: './out3/out3'
				})
			},
			art4() {
				wx.navigateTo({
					url: './out4/out4'
				})
			},
			art5() {
				wx.navigateTo({
					url: './out5/out5'
				})
			},
		}
	}
</script>

<style>
	.page{
		position: relative;
	}
.bg {
	width: 100%;
	height: 808px;
	
}
.bg image{
	width: 100%;
	height: 808px;
}
.article1{
	width: 377px;
	height: 126.5px;	
	position: absolute;
	top: 10%;
	left: 5%;
}

.article2{
	width: 377px;
	height: 126.5px;
	position: absolute;
	top: 28%;
	left: 5%;
}
.article3{
	width: 377px;
	height: 126.5px;
	position: absolute;
	top: 46%;
	left: 5%;
}
.article4{
	width: 377px;
	height: 126.5px;
	position: absolute;
	top: 64%;
	left: 5%;
}
.article5{
	width: 377px;
	height: 126.5px;
	position: absolute;
	top: 82%;
	left: 5%;
}
.article1 image {
	width: 100%;
	height: 126.5px;
}
.article2 image {
	width: 100%;
	height: 126.5px;
}
.article3 image {
	width: 100%;
	height: 126.5px;
}
.article4 image {
	width: 100%;
	height: 126.5px;
}
.article5 image {
	width: 100%;
	height: 126.5px;
}
</style>
