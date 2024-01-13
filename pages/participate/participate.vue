<template>
	<view class="page">
		<view class="bg">
			<image 
			src="https://s2.loli.net/2022/06/24/HcwTIkuFMiRAxUp.png" 
			></image>
		</view>
		<view class="participate1"  @click="part1">
			<image src="https://s2.loli.net/2022/06/25/C34HjN2GOmdhAD5.png" ></image>
			
		</view>
		<view class="participate2" @click="part2">
			<image src="https://s2.loli.net/2022/06/25/LEjJAT2dUXNc1mo.png" ></image>
		</view>
		<view class="participate3" @click="part3">
			<image src="https://s2.loli.net/2022/06/25/YaRdhqDFVw8fSMx.png" ></image>
		</view>
		<view class="participate4" @click="part4">
			<image src="https://s2.loli.net/2022/06/25/uqjaXs8CPvMfntD.png" ></image>
		</view>
		<view class="participate5" @click="part5">
			<image src="https://s2.loli.net/2022/06/25/IihQA5cEZX7SaG9.png" ></image>
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
			part1() {
				wx.navigateTo({
					url: './out1/out1'
				})
			},
			part2() {
				wx.navigateTo({
					url: './out2/out2'
				})
			},
			part3() {
				wx.navigateTo({
					url: './out3/out3'
				})
			},
			part4() {
				wx.navigateTo({
					url: './out4/out4'
				})
			},
			part5() {
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
.participate1{
	width: 377px;
	height: 126.5px;	
	position: absolute;
	top: 10%;
	left: 5%;
}

.participate2{
	width: 377px;
	height: 126.5px;
	position: absolute;
	top: 28%;
	left: 5%;
}
.participate3{
	width: 377px;
	height: 126.5px;
	position: absolute;
	top: 46%;
	left: 5%;
}
.participate4{
	width: 377px;
	height: 126.5px;
	position: absolute;
	top: 64%;
	left: 5%;
}
.participate5{
	width: 377px;
	height: 126.5px;
	position: absolute;
	top: 82%;
	left: 5%;
}
.participate1 image {
	width: 100%;
	height: 126.5px;
}
.participate2 image {
	width: 100%;
	height: 126.5px;
}
.participate3 image {
	width: 100%;
	height: 126.5px;
}
.participate4 image {
	width: 100%;
	height: 126.5px;
}
.participate5 image {
	width: 100%;
	height: 126.5px;
}
</style>
