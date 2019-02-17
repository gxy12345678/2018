<template>
    <div class="app-test">
        <h3>测试组件</h3>
        <p>{{msg}}</p>
        <h3 id="h3">{{msg}}</h3>
    </div>
</template>
<script>
    export default {
        data(){
            return {
                msg:"脚手架"
            }
        },
        methods:{
            show(){
                console.log("执行 show 方法");
            },
            //生命周期
            //创建实例对象  使用   结束
        },
        beforeCreate() {
            //生命周期第一个函数：实例创建之前
            //注意:执行函数data和methods没有初始化
            //console.log(this.msg);   underfined
            //this.show();   报错
        },
        created() {
            //生命周期第二个函数：实例创建之后
            //注意：执行函数data和methods初始化
            console.log(this.msg);
            this.show();
        },
        beforeMount() {
            //生命周期第三个函数：模板已经在内存中编辑完成
            //尚未把模板渲染到页面
            //var h3 = document.getElementById("h3");
            //h3.innerHTML = "123";
        },
        mounted(){
            //生命周期第四个函数：模板已在内存中编辑完成
            //把模板渲染结束
            var h3 = document.getElementById("h3");
            h3.innerHTML = "123123";
        }
    }
</script>
<style>
    .app-test{
        color:red;
    }
</style>