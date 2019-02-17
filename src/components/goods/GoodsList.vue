<template>
  <div class="app-goodslist">
    <!-- 商品列表项 start -->
    <div class="goods-item" v-for="item in list" :key="item.id">
      <img :src="item.img_url" @click="jumpDetail" :data-id="item.id">
      <h3 class="title">{{item.name}}</h3>
      <div class="info">
        <div class="price">
          <span class="now">￥{{(item.price*0.8).toFixed(2)}} </span>
          <span class="old"> ￥{{item.price}}</span>
        </div>
      </div>
      <div class="sell">
        <span>热卖中 </span>
        <span> 剩{{item.bank}}件</span>
      </div>
    </div>
    <!-- 商品列表项 end -->
  </div>
</template>

<script>
export default {
  data(){
    return {
      list:[],
      pageIndex:0,
      pageCount:1,
      pageSize:8
    }
  },
  created() {
    this.getMore();
  },
  methods: {
    jumpDetail(event){
      //获取参数
      var id=event.target.dataset.id;
      //跳转商品详情
      this.$router.push("/GoodsInfo/"+id)
      console.log(id)
    },
    getMore(){
      // 1：创建url地址
      this.pageIndex++;
      var pno=this.pageIndex;
      var ps=this.pageSize;
      var url="http://127.0.0.1:3000/";
      url+="getGoodsList?pno="+pno+"&pageSize";
      url+="="+ps;
      // 2：发送ajax请求
      this.axios.get(url).then(result=>{
        this.list=result.data.data;
        console.log(this.list);
      })
      // 3：获取返回数据 保存list
      // 4：在模板中循环创建数据
    }
  },
}
</script>

<style>
/* 商品列表 */
.app-goodslist{
  display: flex;/* 最外层父元素弹性布局 */
  flex-wrap:wrap;/* 子元素换行 */
  justify-content: space-between;/* 两端对齐 */
  padding: 7px;
}
.app-goodslist .goods-item{
  width: 49%;/* 宽度 */
  border: 1px solid #cccccc;
  box-shadow: 0 0 8px #cccccc;
  margin: 4px 0;
  padding: 2px;
  display: flex;
  flex-direction: column;/* 排列方式：垂直 */
  min-height: 180px;
  justify-content: space-between;/* 子元素两端对齐 */
}
.app-goodslist .goods-item .title{
  font-size: 18px;
}
.app-goodslist .goods-item img{
  width: 100%;
}
/* .app-goodslist .goods-item .price{
  display: flex;
  justify-content: space-between;
} */
.app-goodslist .goods-item .now{
  color: red;
  font-weight: bold;
  font-size: 16px;
}
.app-goodslist .goods-item .old{
  font-size: 12px;
  text-decoration: line-through;
}
.app-goodslist .sell{
  display: flex;
  justify-content: space-between;
  font-size: 14px;
  color: dodgerblue;
}
</style>