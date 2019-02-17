<template>
  <div class="app-goodsinfo">
    <!-- 3：调用子组件 -->
    <!-- 轮播图 -->
    <swiper-box :list="list"></swiper-box>
    <!-- 商品信息 -->
    <div class="mui-card">
      <div class="mui-card-header">
         {{info.name}}
      </div>
      <div class="mui-card-content">
        <div class="mui-card-inner">
           <div class="price">
              市场价:<del>{{info.price}}</del>
              销售价:<span class="now">{{(info.price*0.5).toFixed(2)}}</span>
           </div>
           购买数量:
           	<div class="mui-numbox" data-numbox-min='1' data-numbox-max='9'>
					<button class="mui-btn mui-btn-numbox-minus" type="button" @click="goodsSub">-</button>
					<input id="test" class="mui-input-numbox" type="number" value="1" v-model="val" />
					<button class="mui-btn mui-btn-numbox-plus" type="button" @click="goodsAdd">+</button>
				</div>
        </div>
      </div>
      <div  class="mui-card-footer">
        <mt-button type="primary" size="small">立即购买</mt-button>
        <mt-button type="primary" size="small" @click="addCart">加入购物车</mt-button>
      </div>      
    </div>  
    <!-- 商品参数 -->  
  </div>
</template>

<script>
import {Toast} from "mint-ui";
//1：引入子组件
import swipe from "../sub/swiper.vue";
//2:引入mui组件js文件
//import mui from "../../lib/mui/js/mui.js";
export default {
  //2：注册子组件
  components:{
    "swiper-box":swipe
  },
  created() {
    //console.log("list组件参数:"+this.id);
    this.getImageList();//轮播图
    this.getGoodsInfo();//商品信息
  },
  data(){
    return {
      id:this.$route.params.id,
      list:[],
      val:1,
      info:{}
    }
  },
  methods: {
    getGoodsInfo(){
      //1：获取参数id
      var id = this.id;
      //2：发送ajax请求获取商品信息
      var url = "http://127.0.0.1:3000/getProduct?id="+id;
      //3：保存显示模板
      this.axios.get(url).then(result=>{
        this.info = result.data.data;
        //console.log(this.info)
      });
    },
    addCart(){
      //1：获取参数 uid=1 pid count price
      var uid = 1;//当前登录用户的id
      var pid = this.id;//商品的编号
      var count = this.val;//商品数量
      var price = 999.99;
      //2：发送ajax请求将数据发送服务器
      var url = "http://127.0.0.1:3000/addCart";
      this.axios.get(url,{
        params:{
          uid:uid,
          pid:pid,
          count:count,
          price:price
        }
      }).then(result=>{
        if(result.data.code > 0){
          // 如果商品添加成功，修改全局共享数据数量
          // cartCount
          this.$store.commit("increment");
          //console.log(this.$store.commit("increment"))
          Toast(result.data.msg);
        }else{
          Toast(result.data.msg);
        }
        //console.log(result);
      })
      //3：返回结果
      //4：显示提示消息
    },
    goodsSub(){
      if(this.val > 1){
        this.val--;
      }
    },
    goodsAdd(){
      if(this.val <= 998){
        this.val++;
      }
    },
    getImageList(){
      var url = "http://127.0.0.1:3000/"+"getImages";
      //url += "getImages";
      this.axios.get(url).then(result=>{
        this.list=result.data;
        //console.log(this.list)
      })
    }  
  },
  

}
</script>

<style>

</style>