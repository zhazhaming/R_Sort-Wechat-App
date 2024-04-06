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
						<image src="http://47.115.231.19:8888/group1/M00/00/00/L3PnE2YO4-6AOWMNAAVo3C3Hwf0782.png" mode=""></image>
					</view>
				</swiper-item>
				<swiper-item>
					<!-- 乡村振兴 -->
					<view class="swiper-item" @click="toartcle2">
						<image src="http://47.115.231.19:8888/group1/M00/00/00/L3PnE2YO4ruAIiIpAAgeFMOnzmI593.png" mode=""></image>
					</view>
				</swiper-item>
				<swiper-item>
					<!-- 乡村环境轮播图 -->
					<view class="swiper-item" @click="toartcle3">
						<image src="http://47.115.231.19:8888/group1/M00/00/00/L3PnE2YO44yAHnU3AAcfZY4VBvc116.png" mode=""></image>
					</view>
				</swiper-item>
			</swiper>
		</view>
		<view class="line">
				<!-- 背景 -->
				<image 
					src="http://47.115.231.19:8888/group1/M00/00/00/L3PnE2YO5BOAYyp2AAK8jLDHX1s085.png">
				</image>
		</view>
		<view class="curtain">
			
				<view class="bin1" @click="toEncyclopedias1">
					<!-- 其他垃圾 -->
					<image class="bin"
						src="http://47.115.231.19:8888/group1/M00/00/00/L3PnE2YO2z-AS83BAABb3xBwwQ4581.png">
					</image>
				</view>
				<view class="bin2" @click="toEncyclopedias2">
					<!-- 可回收垃圾 -->
					<image class="bin"
						src="http://47.115.231.19:8888/group1/M00/00/00/L3PnE2YO39OABVNxAABsz5VlYVo288.png">
					</image>
				</view>
				<view class="bin3" @click="toEncyclopedias3">
					<!-- 有害垃圾 -->
					<image class="bin"
						src="http://47.115.231.19:8888/group1/M00/00/00/L3PnE2YO4kaAExI-AAB3IBL0USE771.png">
					</image>
				</view>
				<view class="bin4" @click="toEncyclopedias4">
					<!-- 厨余垃圾 -->
					<image class="bin"
						src="http://47.115.231.19:8888/group1/M00/00/00/L3PnE2YO4n-AFvWQAABUqK109Kk645.png">
					</image>
				</view>
			
			
		</view>
		
		<view class="distinguish">
			<view class="feature">
				<!-- 底部背景 -->
				<image src="http://47.115.231.19:8888/group1/M00/00/00/L3PnE2YO4_-ADSScAAD6lG2h31s764.png" ></image>
			</view>
			<!-- 语言识别 -->
			<image class="distinguish1"
				src="http://47.115.231.19:8888/group1/M00/00/00/L3PnE2YO49eANSEOAAAOJNWk8-0610.png">
			</image>
			<navigator url="/pages/search/search">
				<!-- 文字搜索 -->
				<image class="distinguish2"
					src="http://47.115.231.19:8888/group1/M00/00/00/L3PnE2YO47qARFxZAAANBjBal4g262.png">
				</image>
			</navigator>
			<!-- 拍照识别 -->
			<image class="distinguish3" @click="takePhoto"
				src="http://47.115.231.19:8888/group1/M00/00/00/L3PnE2YO46SATy22AAAQy_4b23M116.png">
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
					// url: 'https://aip.baidubce.com/rest/2.0/image-classify/v2/advanced_general',
					url: 'http://127.0.0.1:5000/api/garbage/identify',
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
						// let result = res.data.result[0].keyword;
						let result = res.data.data.category;
						console.log(result);
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
		top: 27.5%;
		
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
		left: 15%;
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
		left: 48%;
		margin-left: -37.5px;
		top: 20px;
		width: 81px;
		height: 103.5px;
	}
</style>
