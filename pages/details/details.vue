<template>
	<view>
		<view class="bodd">
			
		</view>
		<view class="bg">
			<image 
			src="https://s2.loli.net/2022/06/14/TnZXoY2y6WitwAj.png">
		</image>
		</view>
		<view class="details">
			<view class="header">
				<text class="name">{{item.name}}</text>
				<text class="attr">属于“{{wname}}”</text>
			</view>
			<view class="more">
				<view class="more-title">{{wname}}:</view>
				<view class="more-item">
					<!-- <text>{{item.gexplain}}</text> -->
					<text>{{item.contain}}</text>
					<text>{{item.tip}}</text>
				</view>
			</view>
			<button @click="toSearch">关闭</button>
		</view>
	</view>
</template>

<script>
	var _self
	export default {
		data() {
			return {
				item: [],
				wname: ''
			}
		},
		methods: {
			toSearch() {
				wx.navigateBack({
					url: '../search/search'
				})
			}
		},
		created() {
			_self = this;
		},
		onLoad(options) {
			let title = options.title;
			console.log(title)
			console.log('http://localhost:8009/api/v1/sort/garbagetype/' + title)
			wx.request({
				url: 'http://localhost:8009/api/v1/sort/garbagetype/' + title,
				// url: 'https://api.tianapi.com/lajifenlei/index',
				header: {
					'content-type': 'application/x-www-form-urlencoded'
				},
				// data: {
				// 	key: '5b03bc48fa783f0832d5014fd16afc21',
				// 	word: title
				// },
				success(res) {
					console.log(res.data.code)
					console.log(res.data)
					if(res.data.code==250){
							
						wx.switchTab({
						            url: `/pages/index/index`
						}),
					uni.showToast({
							icon: 'error',
							title: '图片无法识别',
							duration: 2000
						})
						
					}
					else{
						// _self.item = res.data.data[0]
					// _self.item = res.data.newslist[0]
					
					// if (res.data.newslist[0] = 1) {
					// 	_self.wname = '可回收垃圾'
					// } else if (res.data.newslist[0] = 2) {
					// 	_self.wname = '有害垃圾'
					// } else if (res.data.newslist[0] = 3) {
					// 	_self.wname = '厨余垃圾'
					// } else if (res.data.newslist[0] = 4) {
					// 	_self.wname = '其他垃圾'
					// }
						_self.item = res.data.data[0]
						_self.wname = res.data.data[0].gmessage
					}
					
				}
			})
		}
	}
</script>

<style scoped>
	.page{
			position: relative;
			
		}
		.bodd {
			position: absolute;
			top: 0%;
			left: 0%;
			width: 100%;
			height: 808px;
			box-sizing: border-box;
			border: 10px solid rgb(131, 173, 151);
		}
	.bg {
		width: 100%;
		height: 808px;
		
	}
	.bg image{
		width: 100%;
		height: 808px;
	}

	.details {
		position: absolute;
		top: 44rpx;
		left: 0;
	}

	.header {
		padding-top: 120rpx;
		padding-bottom: 100rpx;
		color: #000000;
		display: flex;
		flex-direction: column;
		align-items: center;
	}

	.header text {
		padding: 5rpx 0;
	}

	.name {
		font-size: 25px;
	}

	.attr {
		font-size: 40px;
		font-weight: bold;
	}

	.more {
		width: 90%;
		margin: 0 auto;
		/* background: #fff; */
		/* border-radius: 20rpx; */
		padding: 20rpx;
	}

	.more-title {
		font-size: 20px;
		padding: 10rpx;
	}

	.more-item text {
		font-size: 16px;
		display: block;
		margin-top: 10px;
		color: #fff;
		background: rgb(17, 129, 113);
		border-radius: 40rpx;
		padding: 20rpx;
	}

	button {
		width: 300rpx;
		height: 80rpx;
		background: #fff;
		color: rgb(131, 173, 151);
		border: none;
		line-height: 80rpx;
		font-size: 18px;
		border-radius: 50rpx;
		margin-top: 100rpx;
	}
</style>
