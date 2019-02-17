<template>
    <div class="app-home">
    <!--第一个：顶部状态栏 学子商城-->
        
    <!--第一个：轮播图-->
        <mt-swipe :auto="2500">
            <mt-swipe-item  v-for="item in list" :key="item.id">
                <img :src="item.img_url">
            </mt-swipe-item>
        </mt-swipe>
    <!--第一个：九宫格-->
        <ul class="mui-table-view mui-grid-view mui-grid-9">
		    <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3">
                <router-link to="/NewsList" href="#">
		            <img src="../../img/menu1.png"><span></span>
		            <div class="mui-media-body">新闻资讯</div>
                </router-link>
            </li>
            <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3">
                <a href="#">
		            <img src="../../img/menu2.png"><span></span>
		            <div class="mui-media-body">点餐</div>
                </a>
            </li>
            <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3">
                <router-link to="/GoodsList" href="#">
                    <span class="mui-badge">9</span>
		            <img src="../../img/menu3.png">
		            <div class="mui-media-body">商品</div>
                </router-link>
            </li>
            <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3">
                <a href="#">
		            <img src="../../img/menu4.png"><span></span>
		            <div class="mui-media-body">支付</div>
                </a>
            </li>
            <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3">
                <router-link to="/NewsList">
		            <img src="../../img/menu5.png"><span></span>
		            <div class="mui-media-body">搜索</div>
                </router-link>
            </li>
            <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3">
                <a href="#">
		            <img src="../../img/menu6.png"><span></span>
		            <div class="mui-media-body">更多</div>
                </a>
            </li>
		            
		</ul> 
    <!--第一个：底部导航栏tabbar-->
       
    </div>
</template>
<script>
export default {
    created(){
        //当组件对象创建成功后，即可发送ajax请求
        this.getImages();
    },
    methods:{
        getImages(){
            console.log(123);
            //完成一个功能，获取服务器端轮播图片
            //1.发送ajax请求
            var url = "http://127.0.0.1:3000/getImages";
            this.axios.get(url).then(result=>{
                this.list = result.data;
            })
            //2.获取返回数据保存list
        }
    },
    data(){
        return{
            list:[]
        }
    },

}
</script>
<style>
/*轮播图 */
    .app-home .mint-swipe{
        height:200px;
    }
    .app-home .mint-swipe img{
        width:100%;
    }
    /*九宫格*/ 
    .app-home .mui-grid-9 img{
        width:60px;
        height:60px;

    }
    .app-home .mui-grid-view.mui-grid-9 {
        background-color:#fff;
    }
    .app-home .mui-grid-view.mui-grid-9 li  {
        border:0;
    }
</style>