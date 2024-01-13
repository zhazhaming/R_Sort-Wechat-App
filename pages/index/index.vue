<template>
	<view class="index">
		<!-- <u-swiper :list="list1" indicator indicatorMode="dot" circular height='175' indicator color="rgb(131, 173, 151)"></u-swiper> -->
		
		<view class="uni-margin-wrap" >
			<swiper class="swiper" circular :indicator-dots="indicatorDots" :autoplay="autoplay" :interval="interval"
				:duration="duration" :checked="indicatorDots">
				<!-- <switch @change="changeIndicatorDots" /> -->
				<swiper-item>
					<!-- 垃圾分类轮播图 -->
					<view class="swiper-item" @click="toartcle1">
						<image src="https://picst.sunbangyan.cn/2023/11/18/3273aa4484665c09e417ce2beb9afea6.png" mode=""></image>
					</view>
				</swiper-item>
				<swiper-item>
					<!-- 乡村环境轮播图 -->
					<view class="swiper-item" @click="toartcle2">
						<image src="https://picss.sunbangyan.cn/2023/11/18/ded564a6b10747596314a8b43da04bb3.png" mode=""></image>
					</view>
				</swiper-item>
				<swiper-item>
					<!-- 乡村振兴 -->
					<view class="swiper-item" @click="toartcle3">
						<image src="https://picdm.sunbangyan.cn/2023/11/18/4dd9dc56cd4be7f3b021a500746e8882.png" mode=""></image>
					</view>
				</swiper-item>
			</swiper>
		</view>
		<view class="line">
				<!-- 背景 -->
				<image 
					src="https://picst.sunbangyan.cn/2023/11/18/4bea2504d1618be48fac2b12e66e092e.png">
				</image>
		</view>
		<view class="curtain">
			
			
				<view class="bin1" @click="toEncyclopedias1">
					<!-- 其他垃圾 -->
					<image class="bin"
						src="https://picdl.sunbangyan.cn/2023/11/18/1147de29c0b1b312094f9c27d81bafce.png">
					</image>
				</view>
				<view class="bin2" @click="toEncyclopedias2">
					<!-- 可回收垃圾 -->
					<image class="bin"
						src="https://picdl.sunbangyan.cn/2023/11/18/8d554945acf58b2b69c2ca26e1367514.png">
					</image>
				</view>
				<view class="bin3" @click="toEncyclopedias3">
					<!-- 有害垃圾 -->
					<image class="bin"
						src="https://picst.sunbangyan.cn/2023/11/18/9c1b649df7ebc9db2af900dd1c6bd20e.png">
					</image>
				</view>
				<view class="bin4" @click="toEncyclopedias4">
					<!-- 厨余垃圾 -->
					<image class="bin"
						src="https://picss.sunbangyan.cn/2023/11/18/8cf8fc2d057d76e53f81fbf640b5ed9b.png">
					</image>
				</view>
			
			
		</view>
		
		<view class="distinguish">
			<view class="feature">
				<!-- 底部背景 -->
				<image src="https://picst.sunbangyan.cn/2023/11/18/bb4ca7a26bd52cf7ecf61a2b4bb04f64.png" ></image>
			</view>
			<!-- 语言识别 -->
			<image class="distinguish1"
				src="https://picst.sunbangyan.cn/2023/11/18/024f54781da535a2f7cc0c2405ed5a0d.png">
			</image>
			<navigator url="/pages/search/search">
				<!-- 文字搜索 -->
				<image class="distinguish2"
					src="https://picdl.sunbangyan.cn/2023/11/18/b278ffbc208827262c006afef7d9520d.png">
				</image>
			</navigator>
			<!-- 拍照识别 -->
			<image class="distinguish3" @click="takePhoto"
				src="https://picss.sunbangyan.cn/2023/11/18/b1aaeb027ddbaffbb17bc1971cd8d77d.png">
			</image>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				background: ['color1', 'color2', 'color3'],
				indicatorDots: true,
				autoplay: true,
				interval: 2000,
				duration: 500
				
			}
		},
		onLoad() {
		
		},
		methods: {
			toEncyclopedias1() {
				wx.navigateTo({
					url: '../encyclopedias1/encyclopedias1'
				})
			},
			toEncyclopedias2() {
				wx.navigateTo({
					url: '../encyclopedias2/encyclopedias2'
				})
			},
			toEncyclopedias3() {
				wx.navigateTo({
					url: '../encyclopedias3/encyclopedias3'
				})
			},
			toEncyclopedias4() {
				wx.navigateTo({
					url: '../encyclopedias4/encyclopedias4'
				})
			},
			toartcle1(){
				wx.navigateTo({
					url: '../classify-article/classify-article'
				})
			},
			toartcle2(){
				wx.navigateTo({
					url: '../rural-revitalization/rural-revitalization'
				})
			},
			toartcle3(){
				wx.navigateTo({
					url: '../rural-environment/rural-environment'
				})
			},
			takePhoto() {
				const that = this
				uni.chooseImage({
					count: 1, // 最多可以选择的图片张数，默认9
					sizeType: ['original', 'compressed'], //original 原图，compressed 压缩图，默认二者都有
					sourceType: ['album', 'camera'], //album 从相册选图，camera 使用相机，默认二者都有。如需直接开相机或直接选相册，请只使用一个选项
					success: function(res) {
						wx.getFileSystemManager().readFile({
							filePath: res.tempFilePaths[0],
							encoding: "base64",
							success: childRes => {
								let url = encodeURIComponent(childRes.data)
								that.scanImg(childRes.data)
							},
							fail: err => {
								wx.showToast({
									title: '拍照失败,未获取相机权限或其他原因',
									icon: "none"
								})
							}
						})
					}
				})
			},
			scanImg(base64) {
				const that = this
				wx.showLoading({
					title: '加载数据中....',
				})
				wx.request({
					url: 'https://aip.baidubce.com/rest/2.0/image-classify/v2/advanced_general',
					method: 'POST',
					header: {
						'content-type': 'application/x-www-form-urlencoded'
					},
					data: {
						access_token: '24.d6145f3ab7c004ae77de78be0a43f835.2592000.1659014233.282335-25962792',
						image: base64
					},
					success(res) {
						console.log(res);
						let result = res.data.result[0].keyword;
						wx.hideLoading()
						that.toDetails(result)
					}
				})
			},
			toDetails(result) {
				wx.navigateTo({
					url: '../details/details?title=' + result
				})
			}
		}
	}
</script>

<style scoped>
	.index {
		width: 100%;
		height: 726px;
		background-color: rgb(131, 173, 151);
		position: relative;
	}
	.uni-margin-wrap {
		width: 100%;
		height: 200px;
		z-index: 111;
	}
	.swiper {
		width: 100%;
		height: 200px;
		z-index: 111;
	}
	.swiper-item image {
		width: 100%;
		z-index: 11111;
	}
	.curtain {
		position: absolute;
		margin-left: 5%;
		width: 90%;
		height: 440px;
		background-color: #fff;
	}

	.line {
		width: 100%;
		height: 500px;
		position: absolute;
		left: 0;
		top: 25%;
		
		z-index: 11;
	}
		
	.line image{
		height: 500px;
		width: 100%;
		filter: opacity(80%);
	}
	.bin {
		width: 110.5px;
		height: 140.5px;
	}

	.bin1 {
		position: absolute;
		left: 13%;
		top: 50px;
		z-index: 111;
	}

	.bin2 {
		position: absolute;
		right: 13%;
		top: 50px;
		z-index: 111;
	}

	.bin3 {
		position: absolute;
		left: 13%;
		top: 220px;
		z-index: 111;
	}

	.bin4 {
		position: absolute;
		right: 13%;
		top: 220px;
		z-index: 111;
	}


	

	.distinguish {
		position: relative;
		width: 414px;
		z-index: 111;
		
	}
	.feature{
		
		margin-top: 95%;
		width: 100%;
		height: 100rpx;
		
	}
	.feature image {
		width: 100%;
		height: 218rpx;
	}
	.distinguish1 {
		position: absolute;
		left: 17%;
		top: 40px;
		width: 57.75px;
		height: 77.25px;
	}

	.distinguish2 {
		position: absolute;
		right: 17%;
		top: 40px;
		width: 57.75px;
		height: 77.25px;
	}

	.distinguish3 {
		position: absolute;
		left: 50%;
		margin-left: -37.5px;
		top: 20px;
		width: 81px;
		height: 103.5px;
	}
</style>
