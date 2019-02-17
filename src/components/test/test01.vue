<template>
    <div>
        <h3>test01.vue</h3>
        <h3>方式一：</h3>
        <!--<router-link to="/test02">跳转test02组件<router-link>-->
        <router-link :to="'/test02?id='+id">跳转test02组件</router-link>
        <h3>方式二：</h3>
        <h1 @click="jump">跳转test02组件</h1>
    </div>
</template>
<script>
    export default {
        methods: {
            jump(){
                //this.$router.push("/test02?id="+this.id);
                this.$router.push("/test02/19");
            }
        },
        data(){
            return {
                id:9
            }
        }
    }
</script>
<style>
</style>