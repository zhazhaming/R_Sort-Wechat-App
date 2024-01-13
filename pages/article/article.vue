<template>
	<view class="page">
		<view class="bg">
			<image 
			src="https://s2.loli.net/2022/06/25/WsYVpdzQ2tvqO1B.png" 
			></image>
		</view>
		<view class="article1"  @click="art1">
			<image src="https://s2.loli.net/2022/06/25/MivCjwURWZGq5It.png" ></image>
			
		</view>
		<view class="article2" @click="art2">
			<image src="https://s2.loli.net/2022/06/25/WHtQR6GoCXa74Jv.png" ></image>
		</view>
		<view class="article3" @click="art3">
			<image src="https://s2.loli.net/2022/06/25/BzkTpC7QGW2d9cE.png" ></image>
		</view>
		<view class="article4" @click="art4">
			<image src="https://s2.loli.net/2022/06/25/6Y9psCBV3FTNua7.png" ></image>
		</view>
		<view class="article5" @click="art5">
			<image src="https://s2.loli.net/2022/06/25/qOMauzEfbLX8lpe.png" ></image>
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
