<template>
  <div class="login-container">
    <form> 
      <input type="text" v-model="loginForm.emailOrUsername" placeholder="邮箱/用户名" class="input-field"/>
      <input type="password" v-model="loginForm.password" placeholder="密码" class="input-field"/>
      <button type="submit" class="submit-btn" @click="login">登录</button>
	   <button class="submit-btn" @click="goToRegister">注册</button>
    </form>
    <!-- <p @click="goToRegister">没有帐号点击注册!</p> -->
	<div v-if="loginSuccess" class="popup">
	  <div class="popup-content">
		<h2>登录成功！</h2>
		<p>点击下方按钮跳转到另外一个页面。</p>
		<button @click="closeSuccessMessage">返回首页</button>
	  </div>
	</div>
  </div>
</template>

<script >

export default {
  data() {
    return {
      loginForm: {
        emailOrUsername: '',
        password: '',
      },
	  user: null,
	  loginSuccess: false,
    };
  },
  methods: {
    login() {
		let emailOrUsername = this.loginForm.emailOrUsername;
		let password = this.loginForm.password;
		console.log(emailOrUsername);
		console.log(password);
		uni.request({
			url: `http://localhost:8009/api/v1/user/login?condition=${emailOrUsername}&password=${password}`,
			method: 'POST',
			success:(res) =>{
				if (res.data.code == 200){
					console.log(res.data)
					this.user = res.data.data;
					if (this.user != null){
						this.loginSuccess = true;
					}
				}
			},
		})
    },
	closeSuccessMessage(){
		console.log("点击跳转");
		console.log(this.user)
		wx.redirectTo({
			url: `/pages/user/user?obj=` + JSON.stringify(this.user)
		})
	},
    goToRegister() {
      wx.navigateTo({
      	url: `./register`
      })
    }
  }
};
</script>

<style scoped>
.login-container {
  max-width: 300px;
  margin: 50px auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.input-field {
  width: 100%;
  padding: 20px;
  margin-bottom: 15px;
  border: 1px solid #ddd;
  border-radius: 5px;
  box-sizing: border-box;
}

.submit-btn {
  width: 100%;
  padding: 10px;
  background-color: #5cb85c;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  box-sizing: border-box;
}

.submit-btn:hover {
  background-color: #4cae4c;
}

.switch-form {
  color: #555;
  cursor: pointer;
  text-align: center;
  margin-top: 15px;
}

.switch-form:hover {
  text-decoration: underline;
}

.success-message {
  text-align: center;
  padding: 10px;
  margin-top: 20px;
  background-color: #dff0d8;
  border: 1px solid #d6e9c6;
  border-radius: 5px;
  color: #3c763d;
}

.close-btn {
  background: none;
  border: none;
  color: #3c763d;
  cursor: pointer;
}

.popup {
  position: fixed;
  top: 0;
  left: 0;
  height: 100%;
  width: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}

.popup-content {
  background-color: #fff;
  padding: 20px;
  border-radius: 5px;
  text-align: center;
}

.register-button {
  max-width: 300px;
  margin: 50px auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
}
</style>