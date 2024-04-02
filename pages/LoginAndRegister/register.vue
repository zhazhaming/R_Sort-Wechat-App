<template>
  <div>
    <form >
      <div>
        <input type="text" v-model="registerForm.username" placeholder="用户名" @blur="checkUsername" />
        <span v-if="usernameTaken">已被注册</span>
      </div>
      <div>
        <input type="password" v-model="registerForm.password" placeholder="密码,8-12位" />
      </div>
      <div>
        <input type="email" v-model="registerForm.email" placeholder="邮箱" @blur="checkEmail" />
        <span v-if="emailTaken">已被注册</span>
      </div>
      <button type="submit" :disabled="usernameTaken || emailTaken" @click="register">注册</button>
    </form>
    <p @click="goToLogin">已有帐号立即登录!</p>
    <div v-if="registrationSuccess">
      <p>{{this.registrationMsg}}</p>
      <button @click="closeSuccessMessage">关闭</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      registerForm: {
        username: '',
        password: '',
        email: '',
      },
      usernameTaken: false,
      emailTaken: false,
      registrationSuccess: false,
	  registrationMsg: '',
    };
  },
  methods: {
    checkUsername() {
		let username = this.registerForm.username;
		uni.request({
			url: `http://localhost:8009/api/v1/user/check?condition=${username}`,
			success:(res) =>{
				console.log(res.data)
				this.usernameTaken = res.data.data;
			},
		});
    },
    checkEmail() {
		let email = this.registerForm.email;
		uni.request({
			url: `http://localhost:8009/api/v1/user/check?condition=${email}`,
			success:(res) =>{
				console.log(res.data)
				this.emailTaken = res.data.data;
			},
		});
    },
    register() {
      if (this.usernameTaken || this.emailTaken) {
        return;
      }
	  let username = this.registerForm.username;
	  let email = this.registerForm.email;
	  let password = this.registerForm.password;
	  uni.request({
	  	url: `http://localhost:8009/api/v1/user/register?username=${username}&password=${password}&email=${email}`,
		method:'POST',
		success:(res) =>{
			console.log("11111")
	  		console.log(res.data)
	  		this.registrationSuccess = res.data.data;
	  		this.registrationMsg = res.data.msg;
	  	},
	  });
    },
    closeSuccessMessage() {
      this.registrationSuccess = false;
    },
    goToLogin() {
      wx.navigateTo({
      	url: `./login`
      })
    }
  }
};
</script>
