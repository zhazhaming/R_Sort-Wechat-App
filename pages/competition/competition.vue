
 <template>
 	<view class="content" v-if="controlShow">
 		<!-- <view class="title">环保守卫者挑战赛</view> -->
		<image class="bg"
		src="https://s2.loli.net/2022/06/14/TnZXoY2y6WitwAj.png"></image>
		<view class="zsjd">
			<image 
		src="https://s2.loli.net/2022/06/14/FrlGL8suOCHE7xW.png" ></image>
		</view>
		
 		<view :animation="animationData" class="main-panel">
 			<view class="quesion-panel">
 				<view class="quesion-panel-item1">
 					<view class="quesion-panel-text">{{current+1}}. </view>
 					<view class="quesion-panel-text">
 						{{questionBanks.length>0?questionBanks[current].garbageName:"干电池"}}
 					</view>
 				</view>
 				<view class="quesion-panel-item2">
 					<view class="">属于哪种垃圾分类？</view>
 				</view>
 				<view class="quesion-panel-item3">
 					<view class="gary">（点击下方图标选择）</view>
 				</view>
 				<!-- <view class="quesion-panel-item2">
 					<view class="">{{current+1}}/10</view>
 				</view> -->
 			</view>
 			<view class="main-show-classify">
 				<view class="main-classify">
 					<view @click="switchTabToClassify(1)">
 						<image class="main-img" src="https://s2.loli.net/2022/06/24/VMXhb7nyfcF4tPk.png"></image>
 					</view>
 					<view @click="switchTabToClassify(2)">
 						<image class="main-img" src="https://s2.loli.net/2022/06/24/TBWSgZ6Ljc1MzN3.png"></image>
 					</view>
 				</view>
 				<view class="main-classify">
 					<view @click="switchTabToClassify(3)">
 						<image class="main-img" src="https://s2.loli.net/2022/06/24/ibw1dyXPqYTaQZu.png"></image>
 					</view>
 					<view @click="switchTabToClassify(4)">
 						<image class="main-img" src="https://s2.loli.net/2022/06/14/aN7DOvVwrmc5Ebu.png"></image>
 					</view>
 				</view>
 			</view>
 			<view class="top-text">
 				<view class="">
 					{{current+1}}
 				</view>
 				<view class="gary">
 					/ 10
 				</view>
 			</view>
 		</view>
 
 		<!-- <share /> -->
 	</view>
 </template>
 
 <script>
 	export default {
 		data() {
 			return {
 				questionBanks: [],
 				score: 0,
 				current: 0,
 				controlShow: true,
 				animationData: {},
 			}
 		},
 		onShow() {
 			console.log("size:" + this.questionBanks.length)
 			// let map = new Map();
 			// for (let i = 0; i < 10000; i++) {
 			// 	let temp = Math.round(Math.random() * 10);
 			// 	if (map.has(temp)) {
 			// 		map.set(temp, (map.get(temp)) + 1);
 			// 	} else {
 			// 		map.set(temp, 1);
 			// 	}
 			// }
 			// console.log("size:" + map.size)
 			// for (let [key, value] of map) {
 			// 	console.log(`${key}==${value}`)
 			// }
 			uni.login({
 				provider: 'weixin',
 				success: function(loginRes) {
 					console.log("loginRes")
 					console.log(loginRes);
 					// 获取用户信息
 					uni.getUserInfo({
 						provider: 'weixin',
 						success: function(infoRes) {
 							console.log(infoRes);
 							console.log('用户昵称为：' + infoRes.userInfo.nickName);
 						}
 					});
 				}
 			});
 			this.randTen();
 		},
 		methods: {
 			donghua() {
 				var animation = uni.createAnimation({
 					duration: 1000,
 					timingFunction: 'ease',
 				})
 				this.animation = animation
 				animation.opacity(0).translate(-300).step()
 				this.animationData = animation.export()
 				console.log("1000")
 				setTimeout(function() {
 					animation.translate(10).opacity(0.5).step({
 						duration: 0
 					})
 					this.animationData = animation.export()
 				}.bind(this), 400);
 				setTimeout(function() {
 					animation.translate(0).opacity(1).step({
 						duration: 800
 					})
 					this.animationData = animation.export()
 					console.log("1000")
 				}.bind(this), 500);
 				console.log("动画呢")
 			},
 
 			randTen() {
 				console.log("初始化")
 				if (this.questionBanks.length > 0 && this.current < 9) {
 					return false;
 				}
 				this.current = 0;
 				this.score = 0;
 				this.controlShow = true;
 				this.questionBanks = [];
 				uni.request({
 					// url: 'https://changing.link/sort/garbage-encyclopedia/knowledgeContest',
					url: 'http://localhost:8009/api/v1/sort/garbage-encyclopedia/random',
 					success: (res) => {
 						console.log(res)
						console.log(res.data)
 						console.log(res.data.data);
 						this.questionBanks = res.data.data;
 					}
 				});
 			},
 			switchTabToClassify(index) {
 				if (this.current == 9) this.controlShow = false;
 				console.log(index)
 				console.log(this.questionBanks[this.current])
 				this.questionBanks[this.current]['selectedType'] = index;
 
 				console.log("当前的需要：" + this.current)
 				if (this.questionBanks[this.current].garbageType == index) {
 					this.donghua();
 					let me = this;
 					setTimeout(function() {
 						me.score++;
 						me.current++;
 						me.gotoNav();
 					}, 400);
 
 				} else {
 					let obj = this.questionBanks[this.current];
 					let type = obj.garbageType == 1 ? '其他垃圾' : obj.garbageType == 2 ? '可回收垃圾' : obj.garbageType == 3 ?
 						'厨余垃圾' : '有害垃圾';
 					let temp = obj.garbageName + " 属于 " + type;
 					let me = this;
 					uni.showModal({
 						title: "选错啦",
 						content: temp,
 						confirmText: "知道了",
 						showCancel: false,
 						success: function(res) {
 							console.log(res);
 							console.log("点击了确认:me.current:" + me.current);
 							me.donghua();
 							setTimeout(function() {
 								me.current++;
 								me.gotoNav();
 							}, 400);
 						}
 					})
 				}
 			},
 			gotoNav() {
 				if (this.current >= 10) {
 					console.log("要进行跳转拉")
 					let list = JSON.stringify(this.questionBanks);
 					let score = this.score;
 					uni.request({
 						url: this.serverUrl + '/challenge', //仅为示例，并非真实接口地址。
 						data: {
 							"score": score,
 							"userName": "张三",
 							"list": this.questionBanks
 						},
 						header: {
 							'content-type': "application/json"
 						},
 						method: "POST",
 						success: (res) => {
 							console.log(res)
 							console.log(res.data.data);
 						}
 					});
 					uni.navigateTo({
 						url: `/pages/competition/return/return?score=${score}&list=${list}`
 					});
 				}
 			}
 		}
 	}
 </script>
 
 <style>
	 .content{
	 	width: 100%;
	 	height: 808px;
	 	font-size: 40rpx;
	 	position: relative;
	 	
	 }
	 .bg{
	 	width: 100%;
	 	height:808px;
	 	margin-left: 0;
	 }
	 .zsjd{
	 	width: 100%;
	 	height:402px;
		position: absolute;
		top: 7%;
		left: -5%;
	 }
	 .zsjd image {
		 width: 110%;
		 height: 480px;
	 }
 	.content{
 		/* left: 750upx; */
 		/* position: absolute; */
 		/* width: 700upx; */
 		/* height: 600upx; */
 		/* background-color: #007AFF; */
 	}
 	
 	.top-text {
 		display: flex;
 		flex-direction: row;
 		justify-content: center;
 		margin-bottom: 20upx;
 	
 	}
 	
 	.gary {
 		color: #999999;
 		margin-left: 8upx;
 	}
 	
 	/* 图像显示区  start */
 	.main-classify {
 		display: flex;
 		direction: center;
 		justify-content: center;
 	}
 	
 	.main-img {
 		width: 240upx;
 		height: 240upx;
 		padding: 20upx;
 	}
 	
 	/* 图像显示区  end */
 	.title {
 		text-align: center;
 		margin: 20upx auto;
 		font-size: 40upx;
 		/* color: #72c69c; */
 	
 	}
 	
 	.main-panel {
		position: absolute;
		top: 10%;
 		left: 15%;
		
 	}
 	
 	.quesion-panel {
 		display: flex;
 		flex-direction: column;
 		margin: 20upx 0 0 0;
 		font-size: 40rpx;
 	
 	}
 	
 	.quesion-panel-item1 {
 		display: flex;
 		flex-direction: row;
 		justify-content: center;
 		align-items: center;
 		margin-bottom: 20upx;
 		
 	}
 	
 	.quesion-panel-item2 ,.quesion-panel-item3 {
 		display: flex;
 		flex-direction: row;
 		justify-content: center;
 	}
 	.quesion-panel-item3 .gary{
 		font-size: 30upx;
 		margin-top: 10upx;
 	}
 	
 	.quesion-panel-text {
 		color: #e96900;
 		font-size: 46upx;
 		margin-right: 20upx;
 	}
 	
 </style>
 