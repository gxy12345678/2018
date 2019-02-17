<template>
  <div class="app-register">
    <div class="mui-card-header">
      <h3>用户注册</h3>
    </div>
    <div class="mui-card-content">
      <div class="mui-card-content-inner">
        <form action="">
          用户名：<input type="text" value="" placeholder="请输入用户名" v-model="name" @blur.prevent="checkName">
          密码：<input type="password" value="" placeholder="请输入密码" v-model="pwd">
          确认密码：<input type="password" value="" placeholder="请输入确认密码" v-model="pwd2">
          <mt-button type="primary" size="large" @click="handleReg">注册</mt-button>
        </form>
      </div>
    </div>
    <div class="mui-card-footer"></div> 
  </div>
</template>

<script>
import {Toast} from "mint-ui";
export default {
  created() {
    //this.handleReg();
  },
  data(){
    return {
      name:"", //准备双向绑定的数据
      pwd:"",
      pwd2:"",
      isSubmit:false //是否允许提交
    }
  },
  methods: {
    checkName(){
      //1：获取用户输入的用户名
      var n = this.name;
      //2：发送ajax请求
      var url = "http://127.0.0.1:3000/existsName?name="+n;
      this.axios.get(url).then(result=>{
        //3：提示消息
        Toast(result.data.msg);
        if(result.data.code > 0){
          this.isSubmit = true;
        }else{
          this.isSubmit = false;
          //Toast(result.data.msg);
        }
      })
    },
    handleReg(){
      if(!this.isSubmit){//禁止提交
        Toast("用户名已存在，请修改")
        return;
      }
      //1：获取用户输入用户名 密码 确认密码
      //  双向绑定
      var n = this.name;
      var p = this.pwd;
      var p2 = this.pwd2;
      //2：验证
      var regname = /^[a-z0-9]{8,12}$/i;
      var regpwd = /^[a-z0-9]{6,12}$/i;
      //验证用户名
      if(!regname.test(n)){
        Toast("用户名格式不正确");
        return
      }
      //验证密码
      if(!regpwd.test(p)){
        Toast("密码格式不正确");
        return
      }
      //验证密码和确认密码一致
      if(p != p2){
        Toast("两次密码不一致，请修改");
        return
      }
      //3：发送ajax请求
      var url = "http://127.0.0.1:3000/Register?name="+n+"&pwd="+p;
      this.axios.get(url).then(result=>{
        //4：提示
        Toast(result.data.msg);        
      })
    }
  },
}
</script>
<style>

</style>