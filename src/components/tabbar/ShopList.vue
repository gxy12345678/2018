<template>
  <div class="app-shoplist">
    <div class="mui-card-header">
      <h3>购物车列表</h3>
    </div>
    <div class="mui-card-content">
      <div class="mui-card-content-inner">
        <!-- 商品的项目 start -->        
        <ul>
          <li class="mui-table-view-cell mui-media" v-for="item in list" :key="item.id">
            <!-- <a href="javascript:;">
						  <img class="mui-media-object mui-pull-left" :src="item.img_url">
						    <div class="mui-media-body">
							    {{item.name}}
							    <p class='mui-ellipsis'><small>￥</small>{{item.price}}</p>
						    </div>  
					  </a> -->
            <div class="mui-input-row">
							<label>
                <a href="javascript:;">
						      <!-- <img class="mui-media-object mui-pull-left" :src="item.img_url"> -->
						      <div class="mui-media-body">
							    {{item.name}}
							      <p class='mui-ellipsis'><small>￥</small>{{item.price}}</p>
						      </div>  
					      </a>
              </label>
							<div class="mui-numbox">
								<button class="mui-btn mui-btn-numbox-minus" type="button" @click="cartSub" :data-id="item.id">-</button>
								<input class="mui-input-numbox" type="number" :value="item.count"/>
								<button class="mui-btn mui-btn-numbox-plus" type="button" @click="cartAdd" :data-id="item.id">+</button>
							</div>
						</div>
				  </li>
          <!-- 商品的项目  end -->
        </ul>
      </div>
    </div>
    <div class="mui-card-footer">
      小计：￥{{getSubTotal}}
    </div> 
  </div>
</template>

<script>
export default {
  created() {
    this.getList();
  },
  //累加求和购物车的小计
  computed: {
    getSubTotal:function(){
      var sum = 0;
      for(var item of this.list){
        sum += item.price * item.count;
      }
      return sum.toFixed(2);
    }
  },
  data(){
    return {
      list:[],
      sum:0
      //name:"",
      //price:"",
    }
  },
  methods: {
    updateItemCount(id,count){
      var url = "http://127.0.0.1:3000/updateCart?id="+id+"&count="+count;
      this.axios.get(url).then(result=>{
        //console.log(result);
      });
    },
    cartSub(e){
      var id = e.target.dataset.id;
      for (var item of this.list){
        if (item.id == id&&item.count > 1){//数量不能小于1
          item.count--;
          //同步数据
          this.updateItemCount(item.id,item.count);
          break;
        }
      }
    },
    cartAdd(e){
      //1：获取当前按钮绑定购物车id
      var id = e.target.dataset.id;
      //2：创建循环购物车数组内容
      for (var item of this.list){
      //3：判断当前元素id是否与元素id相同
        if (item.id == id){
          //4：修改数据
          item.count++;
          //同步数据
          this.updateItemCount(item.id,item.count);
          break;
        }
      }
    },
    getList(){
      var url = "http://127.0.0.1:3000/getCartList";
      this.axios.get(url).then(result=>{
        console.log(result);
        this.list = result.data.data;    
      })
    }
  },
}
</script>

<style>
.mui-media a img.mui-pull-left{
  width: 100%;
}
.mui-media label a img{
  width: 100%;
}

</style>