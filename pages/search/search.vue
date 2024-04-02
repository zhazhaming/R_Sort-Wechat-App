<template>
	<view class="page">
		<view class="bodd">
			
		</view>
		<view class="bg">
			<image 
			src="https://s2.loli.net/2022/06/14/TnZXoY2y6WitwAj.png">
		</image>
		</view>
		
		<view class="container">
			<!-- <view class="top">
				<text class="top-title">这是什么垃圾</text>
				<text class="top-more">一键查询免烦恼，从我做起爱环保</text>
			</view> -->
			<view class="search">
				<view class="search-main">
					<input  @input="iptDetails" v-model="clean" />
				</view>
				<view class="search-list" v-if="searchList.length>0">
					<text  v-for="item in searchList" @click="toDetails" :data-title='item.garbageName'>{{item.garbageName}}</text>
				</view>
				<view class="search-list" v-else-if="showResultMessage">
					<text >暂无查询到结果</text>
				</view>
			</view>
			<view class="hot">
				<view class="hot-search">
					<!-- 热门搜索 -->
					<img src="https://picss.sunbangyan.cn/2024/01/13/cb1df4f85b2419ea1f1c4f886c9c9713.jpeg" alt="">
				</view>
				<view class="hot-item">
					<text v-for="item in hotSearch.slice(0,10)" @click="toDetails"
						:data-title='item.garbageName'>{{item.garbageName}}</text>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	var _self
	export default {
		data() {
			return {
				hotSearch: [],
				searchList: [],
				showResultMessage: false,  //显示“暂无查询结果”文本
				isRequest: true,  //当输入框中没有文本，则设置为fasle不请求接口
			}
		},
		methods: {
			toDetails(e) {
				let title = e.currentTarget.dataset.title;
				wx.navigateTo({
					url: '../details/details?title=' + title
				})
			},
			iptDetails(e) {
				let val = e.detail.value;
				if (val.length == 0) {
					_self.searchList = [];
					this.showResultMessage = false;
					this.isRequest = false;
				}else{
					this.isRequest = true;
				}
				if (this.isRequest){
					wx.request({
						url: 'http://localhost:8009/api/v1/sort/garbage-encyclopedia/name/' + val,
						// url: 'https://api.tianapi.com/lajifenlei/index',
						// header: {
						// 	'content-type': 'application/x-www-form-urlencoded'
						// },
						// data: {
						// 	key: '5b03bc48fa783f0832d5014fd16afc21',
						// 	word: val
						// },
						success(res) {
							_self.searchList = res.data.data;
							_self.showResultMessage = _self.searchList.length <= 0;
							// _self.searchList = res.data.newslist
							// console.log(_self.searchList)
						}
					})
				}
				
			}
		},
		created() {
			_self = this;
		},
		onLoad() {
			wx.request({
				url: 'http://localhost:8009/api/v1/sort/garbage-encyclopedia/random',
				// url: 'https://api.tianapi.com/hotlajifenlei/index',
				// header: {
				// 	'content-type': 'application/x-www-form-urlencoded'
				// },
				// data: {
				// 	key: '5b03bc48fa783f0832d5014fd16afc21',
				// },
				success(res) {
					console.log(res);
					_self.hotSearch = res.data.data
					// _self.hotSearch = res.data.newslist
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
	.container {
		position:absolute;
		left: 0;
		top: 88rpx;
	}

	/* .top {
		display: flex;
		align-items: center;
		flex-direction: column;
		color: #000000;
		padding-top: 150rpx;
	} */

	.top-title {
		font-size: 36px;
		font-weight: bold;
	}

	.top-more {
		font-size: 16px;
	}

	.search {
		padding-top: 40rpx;
		display: flex;
		justify-content: center;
	}

	.search-main {
		display: flex;
	
		align-items: center;
		background: #fff;
		border-radius: 40rpx;
		border: 4px dashed rgb(91, 140, 137);
		
		height: 80rpx;
		width: 90%;
	}

	

	.search-main input {
		flex: 1;
		padding-left:2em ;
		font-size: 16px;
	}

	.search-list {
		display: flex;
		flex-direction: column;
		overflow-y: auto;
		background: #fff;
		width: 90%;
		height: 900rpx;
		position: fixed;
		border-radius: 40rpx;
		top:13%;
		bottom: 0;
		z-index: 999;
		padding: 30rpx;
	}

	.search-list text {
		padding: 20rpx 0;
		border-bottom: 1px solid #f5f5f5;
		font-size: 16px;
		color: #000000;
	}

	.hot {
		width: 90%;
		background: rgba(251, 253, 250, 0.6);
		border-radius: 40rpx;
		padding-top: 5rpx;
		padding-bottom: 10rpx;
		margin-left: 5%;
		margin-top: 15%;
		color: #000000;
	}

	.hot-search {
		width: 96.5px;
		height: 24px;
		padding: 40rpx;
		text-decoration: underline;
	}
	.hot-search img {
		width: 100%;
		height: 24px;
	}
	.hot-item {
		padding: 0 40rpx;
		display: flex;
		flex-wrap: wrap;
	}

	.hot-item text {
		height: 50rpx;
		border-radius: 30rpx;
		background-color: rgba(152, 184, 183,0.6);
		border: 1px solid #e1e1e1;
		padding: 5rpx 30rpx;
		font-size: 16px;
		margin: 20rpx 20rpx 20rpx 0;
	}
</style>
