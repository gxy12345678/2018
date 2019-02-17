<template>
  <div class="app-login">
    <div class="mui-card-header">
      <h3>用户登录</h3>
    </div>
    <div class="mui-card-content">
      <div class="mui-card-content-inner">
        <form action="">
          用户名：<input type="text" value="" placeholder="请输入用户名" v-model="name">
          密码：<input type="password" value="" placeholder="请输入密码" v-model="pwd">
          <mt-button type="primary" size="large" @click.prevent="handleLogin">登录</mt-button>
        </form>
      </div>
    </div>
    <div class="mui-card-footer"></div>    
  </div>
</template>

<script>
import {Toast} from "mint-ui";
export default {
  data(){
    return {
      name:"",
      pwd:"",
    }
  },
  methods: {
    handleLogin(){
      //1：获取用户输入的用户名和密码
      var n = this.name;
      var p = this.pwd;
      //2：验证
      var reg = /^[a-z0-9]{3,12}$/i
      //3：验证失败提示消息
      if(!reg.test(n)){
        Toast("用户名格式不正确");
        return
      }
      if(!reg.test(p)){
        Toast("密码格式不正确");
        return
      }
      //4：发送ajax请求
      var url = "http://127.0.0.1:3000/login?name="+n+"&pwd="+p;
      this.axios.get(url).then(result=>{
        console.log(result.data)
        //5：如果登录成功 跳转/Home
        if(result.data.code == 1){
          Toast(result.data.msg);
          this.$router.push("/Home");
        }else{//6：如果失败 提示消息
          Toast(result.data.msg);
        }
      })
    }
  },
}
</script>

<style>

</style>