<template>
	<view class="user">
		<view>
			<image class="header" src="https://s2.loli.net/2022/06/14/1E7tKWlq6XZvujz.png">
			</image>
		</view>
		<view class="_abbr">
			<view class="line">
				<!-- 背景 -->
				<img src="https://s2.loli.net/2022/06/14/PQnDaybdW3cmI7G.png" alt="">
			</view>
			<view class="bin1" @click="toEncyclopedias1">
				<!-- 签到 -->
				<image class="bin" src="https://s2.loli.net/2022/06/27/ubityYNIce6r9wf.png">
				</image>
			</view>
			<view class="bin2" @click="toEncyclopedias2">
				<!-- 客服 -->
				<image class="bin" src="https://s2.loli.net/2022/06/14/pykYIPlSotivcW8.png">
				</image>
			</view>
			<view class="bin3">
				<!-- 积分 -->
				<image class="bin" src="https://s2.loli.net/2022/06/27/hzV1GZAkmKqEj3T.png">
					
				</image>
				<view class="num">
					{{number}}
					
				</view>
			</view>
			<view class="bin4" @click="toEncyclopedias3">
				<!-- 关于我们 -->
				<image class="bin" src="https://s2.loli.net/2022/06/14/cuzj8AEPrSvgint.png">
				</image>
			</view>

			<!-- style="position: absolute; top: 0; left: 0;" -->
			<!-- 头像 -->
			<view class="users">
				<view class="u-avatar" @click="getUserProfile">
					<image :src="avatarUrl" style="background-color: #868686;">

					</image>
				</view>

				<text>{{nickName}}</text>

			</view>


			<!-- 昵称 -->



		</view>
	</view>

</template>

<script>
// import { data } from 'jquery';
	export default {
		data() {
			return {
				avatarUrl: '',
				nickName: '点击头像登录',
				isLogin: 0,
				number: 0,
				time: '',
				isSign: false,
				userinfo:{
					username: "",
					geneder: "",
					img_url: "",
					appid: "",
					appSceret: "",
					code: ""
				}
			};
		},
		methods: {
			async getUserProfile() {
			  const that = this;
			  const appid = "wx8b5515246d31aede";
			  const appsceret = "e94d75e317a404349bd1fbc36aef8b87";
			  try {
			    // 获取用户个人信息
			    const userProfile = await new Promise((resolve, reject) => {
			      wx.getUserProfile({
			        desc: '用于完善资料',
			        success: (res) => {
			          console.log(res);
			          that.avatarUrl = res.userInfo.avatarUrl;
			          that.nickName = res.userInfo.nickName;
			          that.isLogin = 1;
			          that.userinfo.username = that.nickName;
			          that.userinfo.gender = res.userInfo.gender;
			          that.userinfo.img_url = res.userInfo.avatarUrl;
			          that.userinfo.appid = appid;
			          that.userinfo.appSceret = appsceret;
			          resolve(res.userInfo);
			        },
			        fail: reject
			      });
			    });
			
			    // 登录获取 code
			    const loginResult = await new Promise((resolve, reject) => {
			      wx.login({
			        success: (res) => {
			          if (res.code) {
			            console.log(res.code);
			            that.userinfo.code = res.code;
			            resolve(res.code);
			          } else {
			            reject(new Error('登录失败！' + res.errMsg));
			          }
			        },
			        fail: reject
			      });
			    });
			
			    // 发起请求
			    const requestResult = await new Promise((resolve, reject) => {
			      wx.request({
			        url: 'http://localhost:8009/api/v1/user/wx_login',
			        method: 'POST',
			        data: that.userinfo,
			        success: (res) => {
						
						that.number = res.data.data.score;
						if (res.data.data.sign == 1){
							that.isSign = true
						}
						console.log(that.isSign)
			              resolve(res);
			            },
			            fail: reject
			      });
			    });
			    console.log('请求成功', requestResult.data);
			  } catch (error) {
			    console.error('发生错误', error);
			  }
			},
			// onLoad(options){
			// 	var userInfo = JSON.parse(options.obj);
			// 	console.log("进入自动加载函数");
			// 	if (userInfo != null){
			// 		this.avatarUrl = userInfo.imgUrl;
			// 		this.nickName = userInfo.username;
			// 		this.number = userInfo.score;
			// 		this.isLogin = 1;
			// 		if(userInfo.sign == 1){
			// 			this.isSign = true;
			// 		}
			// 	}
			// },
			// getUserProfile(){
			// 	wx.navigateTo({
			// 		url: `/pages/LoginAndRegister/login`
			// 	})
			// },
			toEncyclopedias2(){
				wx.navigateTo({
					url: `/pages/user/contact/contact`
				})
			},
			toEncyclopedias3(){
				wx.navigateTo({
					url: `/pages/user/our/our`
				})
			},
			toEncyclopedias1() {
				console.log(this.isLogin)
				if (this.isLogin == 0) {
					uni.showToast({
						icon: 'error',
						title: '请先登录',
						duration: 2000
					});
				}

				if (this.isLogin == 1 && this.isSign == false) {
					uni.request({
						url: `http://localhost:8009/api/v1/user/updateScore?username=${this.nickName}&score=5`,
						method:'POST',
						success:(res) =>{
							if (res.data.code == 200){
								this.isSign = true;
								this.number = res.data.data;
								if (this.isSign){
									uni.showToast({
										icon: 'success',
										title: '签到成功',
										duration: 2000
									});
								}
							}
						},
					})
					}else {
						uni.showToast({
							icon: 'error',
							title: '今日已签到',
							duration: 2000
						});
					} 
				}
			}
		}
</script>

<style scoped>
	.user {
		width: 100%;
		height: 808px;
		background-color: rgb(225, 246, 234);
		position: relative;
	}

	.header {
		width: 90%;
		height: 500rpx;
		margin-top: 2%;
		margin-left: 5%;
	}

	.users {
		width: 100%;
		height: 200px;
		position: absolute;
		top: -13%;
		left: 0%;
		text-align: center;
	}

	.u-avatar {
		width: 115.2px;
		height: 115.2px;
		margin: 0 auto;

	}

	.u-avatar image {
		width: 100%;
		height: 115.2px;
		border-radius: 10em;
	}

	._abbr {
		width: 80%;
		height: 400px;
		background-color: rgb(255, 255, 255);
		/* background: url(https://s2.loli.net/2022/06/14/PQnDaybdW3cmI7G.png); */
		border-radius: 8%;
		position: absolute;
		top: 220px;
		left: 10%;
	}

	.line img {
		width: 100%;
		height: 400px;
	}

	.bin {
		width: 100px;
		height: 100px;
	}

	.bin1 {
		position: absolute;
		left: 13%;
		top: 120px;
	}

	.bin2 {
		position: absolute;
		right: 13%;
		top: 120px;
	}

	.bin3 {
		position: absolute;
		left: 13%;
		top: 250px;
	}
	.num {
		position: absolute;
		left: 60%;
		top: 70%;
		color: rgb(163, 171, 170);
	}
	.bin4 {
		position: absolute;
		right: 13%;
		top: 250px;
		
	}
</style>
