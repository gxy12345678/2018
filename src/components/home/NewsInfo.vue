<template>
    <div class="app-newsinfo">
        <h3>{{info.title}}</h3>
        <h5>{{info.ctime | datetimeFilter}}</h5>
        <p>{{info.content}}</p>
        <!--(3).调用评论子组件-->
        <comment-box :id="id"></comment-box>
    </div>
</template>
<script>
    //(1).引入评论子组件
    import comment from "../sub/comment.vue"
    export default{
        created(){
            //console.log(this.$route.query.id );
            //调用函数
            this.getNewsInfo();
        },
        methods: {
            //创建函数
            getNewsInfo(){   
                //1.获取参数 id
                var id = this.$route.query.id;
                //2.创建变量保存   url地址
                var url = "http://127.0.0.1:3000/getNewsInfo?id="+id;
                //3.发送ajax请求获取数据
            
                //4.将返回结果保存  info对象
                this.axios.get(url).then(result=>{
                    this.info=result.data.data;      
                })
            }
        },
        data(){
            return {
                info:{},
                id:this.$route.query.id
            }  
        },
        //(2).注册子组件
        components:{
            "comment-box":comment//注册评论子组件
        },
    }
</script>
<style>
    .app-newsinfo{
        background-color:#fff;
        border:1px solid #aaa;
    }
    .app-newsinfo h3{
        font-size:18px;
    }
    .app-newsinfo p{
        font-size:14px;
    }
</style>