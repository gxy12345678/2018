<template>
    <div class="app-comment">
        <h3>评论子组件</h3>
        <!-- 发表评论区 -->
        <textarea placeholder="请吐槽最多120个字" maxlength="120" v-model="msg"><!--双向绑定 --></textarea>
        <mt-button size="large" @click="addComment">发表评论</mt-button>
        <!--显示评论区域-->
        <div class="cmt-list">
            <div class="cmt-item" v-for="(item,i) in list" :key="item.id">
                第 {{i+1}} 楼：发表时间 {{item.ctime | datetimeFilter}}
                <div class="cmt-body">
                    {{item.content}}
                </div>
            </div>
        </div>
        <mt-button size = "large" @click="getMore">加载更多</mt-button>
    </div>
</template>
<script>
//独立引入mintui库中的一个组件
import {Toast} from "mint-ui"
export default {
  data(){
    return {
      msg:"",       //双向绑定
      pageIndex:0,  //当前页码
      pageSize:7,   //页大小
      pageCount:1,  //总页数
      list:[]       //当前页内容
      }
  },
  methods:{
    getMore(){
      //1.获取新闻编号  nid  pno pageSize
      var nid = this.nid;
      this.pageSize++;
      var pno = this.pageIndex;
      var ps = this.pageSize;
      //2.当前页码自增
      //3.创建变量  url
      var url="http://127.0.0.1:3000/getComments?pno="+pno+"&nid="+nid+"&pageSize="+ps;
      //4.发送ajax请求
      this.axios.get(url).then(result=>{
        //console.log(result);
        //5.获取返回数据   追加
        //console.log(this.list);
        var rows = this.list.concat(result.data.data);
        this.list = rows;
      }) 
    },
    addComment(){
      //1.获取两个参数nid content
      var nid = this.id;
      var content = this.msg;
      var size = content.trim().length;//内容的长度
      if (size == 0){
        Toast("评论内容不能为空");
        return;
      };
      //2.发送ajax请求
      var url="http://127.0.0.1:3000/addComment?nid="+nid+"&content="+content;
      //3.接收返回数据
      this.axios.get(url).then(result=>{
      if(result.data.code == 1){
        Toast(result.data.msg);
        this.msg="";//清空发表内容
        //获取最新评论结果分页
        this.list=[];//清空原有的数据
        this.pageIndex=0;//清空页码
        this.getMore()
      }else{
        Toast(result.data.msg);
      }
    });
    //4.Toast();
    }
    },
    props:["id"],
    created(){
        //console.log(this.id);
        this.getMore();
    }
}
</script>
<style>
 .app-comment h3{
     font-size:18px;
 }
 .app-comment textarea{
     font-size:14px;
     height:60px;
     margin:0;
 }
 /*评论列表*/
 .app-comment .cmt-list{
     margin:5px;
 }
 .app-comment .cmt-list .cmt-item{
     border:1px solid #aaa;
     margin-top:15px;
 }
</style>