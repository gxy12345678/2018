<template>
  <div>
    <h1>推出登录</h1>
    <mt-button @click="logout">退出登录</mt-button>
  </div>
</template>
<script>
import {Toast} from "mint-ui";
export default {
  data(){
    return{}
  },
  methods:{
    logout(){
      var url="http://127.0.0.1:3000/logout";
      this.axios.get(url).then(resul=>{
        Toast("退出成功")
      })
    }
  }
}
</script>