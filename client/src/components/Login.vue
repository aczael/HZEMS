<template>
<div>
    <input v-model="user.username" placeholder="用户名">
    <input v-model="user.password" placeholder="密码">
    <button @click='handleLogin'>登录</button>
    <div>{{user.username}}</div>
    <div>{{user.password}}</div>
</div>
</template>

<script>
export default {
  name: 'Login',
  data(){
    return {
      msg: 'Welcome to Your Vue.js App',
      user:{
        username:'',
        password:''
      }
    }
  },
  methods:{
    handleLogin(){
        console.log(this.user)
        let _this = this;
         this.$axios({
        method: "POST",
        url: `http://localhost:3000/api/login`,
        data: this.user,
        headers: {
            'Content-Type': 'application/json'
         
        }
    })
    .then(function (response) {
           
           
           _this.userToken = 'Bearer ' + response.data.token;
           console.log( _this.userToken);
           //存入本地token


        })
        .catch(function (error) {
            console.log(error);
        })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
