<template>
	<view>
		<view class="background">
			<view>
				<!-- 文章 -->
				<image class="article" src="http://47.115.231.19:8888/group1/M00/00/00/L3PnE2YQuBuADb22AAASLKmbIoo674.png" @click="toarticle"></image>
				<!-- 参与 -->
				<image class="participate" src="http://47.115.231.19:8888/group1/M00/00/00/L3PnE2YQuCmANJy5AAAZVAjzVpA657.png" @click="toparticipate"></image>
				<!-- 知识竞答 -->
				<image class="competition" src="http://47.115.231.19:8888/group1/M00/00/00/L3PnE2YQuAuATA2GAAAU7HMlEhQ686.png" @click="tocompetition"></image>
<!-- 				<image class="game" src="https://636c-cloud1-5gy3mgvy401e933b-1306354275.tcb.qcloud.la/game.png?sign=7a8d8a3793d6be8093d343731f74b01c&t=1644754338"></image> -->
			</view>
			<view class="background1"></view>
		</view>
		<view class="video">
				<video wx:if="videoList && videoList.length > 0" class="video1" :src="videoList[0]"></video>
			    <video wx:if="videoList && videoList.length > 1 " class="video2" :src="videoList[1]"></video>
			    <video wx:if="videoList && videoList.length > 2" class="video3" :src="videoList[2]"></video>
			    <video wx:if="videoList && videoList.length > 3" class="video4" :src="videoList[3]"></video>
			</view>
		</view>
	</view>
</template>

<script>
// import { get } from 'jquery'
// import { methods } from '../../uni_modules/uview-ui/libs/mixin/mixin'
	export default {
		data() {
			return {
				videoList: []
			}
		},
		onLoad(){
			console.log("自动加载视频")
			uni.request({
				url: `http://localhost:8009/api/v1/images/randomVideo?pageSize=4`,
				success:(res) =>{

					if (res.data.code == 200){
						this.videoList = res.data.data;
					}
				}
			})
		},
		methods: {
			
			toparticipate() {
				console.log("点击了参与列表")
				wx.navigateTo({
					url: '../participate/participate_new'
				})
			},
			toarticle() {
				console.log("进入了文章列表")
				wx.navigateTo({
					url: '../article/article_new'
				})
			},
			tocompetition() {
				wx.navigateTo({
					url: '../competition/competition'
				})
			},
		}
	}
</script>

<style scoped>
	.background {
		width: 100%;
		height: 500px;
		background-image: url(https://picst.sunbangyan.cn/2024/01/27/11010188ad9d70f7d538f44ab8026322.jpeg);
		background-size: 100% 100%;
		position: relative;
	}
	
	.background1 {
	    width: 90%; /* 背景图的宽度占页面宽度的90% */
	    height: 25%; /* 背景图的高度占页面高度的15% */
	    position: absolute; /* 使用绝对定位 */
	    top: 75%; /* 上边距为页面高度的50%，使其垂直居中 */
	    left: 5%; /* 左边距为页面宽度的3% */
	    transform: translateY(-50%); /* 通过负的上边距来实现垂直居中 */
	    z-index: 0; /* 设置层级为1，置于第二层图层 */
	    background-image: url(http://47.115.231.19:8888/group1/M00/00/00/L3PnE2YQuDiAYNOEAABK1UkLVuw256.png); /* 背景图的 URL */
	    background-size: cover; /* 背景图尺寸设置为 cover，保持图片比例并填充容器 */
	    background-position: center; /* 背景图在容器中居中显示 */
	    background-repeat: no-repeat; /* 背景图不重复 */
	}

	.participate {
		width: 50px;
		height: 64.5px;
		position: absolute;
		top: 350px;
		left: 20%;
		z-index: 1;
	}

	.article {
		width: 50px;
		height: 64.5px;
		position: absolute;
		top: 350px;
		left: 45%;
		z-index: 1;
	}

	.competition {
		width: 50px;
		height: 64.5px;
		position: absolute;
		top: 350px;
		right: 20%;
		z-index: 1;
	}

	.game {
		width: 46px;
		height: 60.5px;
		position: absolute;
		top: 350px;
		right: 35%;
	}

	.video {
		width: 100%;
		height: 200px;
		background-image: url(https://picss.sunbangyan.cn/2024/01/27/f035eebe7f4a29002bca8a4b0e07e166.jpeg);
		background-size: 100% 100%;
		position: relative;
		margin-top: -50px;
	}

	.video1 {
		position: absolute;
		top: 50px;
		left: 20px;
		width: 170px;
		height: 100px;
	}

	.video2 {
		position: absolute;
		top: 50px;
		right: 20px;
		width: 170px;
		height: 100px;
	}

	.video3 {
		position: absolute;
		top: 200px;
		left: 20px;
		width: 170px;
		height: 100px;
	}

	.video4 {
		position: absolute;
		top: 200px;
		right: 20px;
		width: 170px;
		height: 100px;
	}
</style>
