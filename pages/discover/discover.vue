<template>
	<view>
		<view class="background">
			<view>
				<image class="article" src="https://picst.sunbangyan.cn/2024/01/27/f9a1a37a63d4b157ae801cf576ec31ea.jpeg" @click="toarticle"></image>
				<image class="participate" src="https://picdm.sunbangyan.cn/2024/01/27/d039943c277f6dd938403b71a8ae4621.jpeg" @click="toparticipate"></image>
				<image class="competition" src="https://picdm.sunbangyan.cn/2024/01/27/5a09c7f2e437043768baf097fa6d38eb.jpeg" @click="tocompetition"></image>
				<!-- <image class="game" src="https://636c-cloud1-5gy3mgvy401e933b-1306354275.tcb.qcloud.la/game.png?sign=7a8d8a3793d6be8093d343731f74b01c&t=1644754338"></image> -->
			</view>
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
					url: '../article/article'
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

	.participate {
		width: 50px;
		height: 64.5px;
		position: absolute;
		top: 350px;
		left: 20%
	}

	.article {
		width: 50px;
		height: 64.5px;
		position: absolute;
		top: 350px;
		left: 45%;
	}

	.competition {
		width: 50px;
		height: 64.5px;
		position: absolute;
		top: 350px;
		right: 20%;
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
