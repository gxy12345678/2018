<template>
    <div>
        <h3>test02.vue</h3>
    </div>
</template>
<script>
    export default {
        created() {
            //console.log(this.$route.query.id);
            console.log(this.$route.params.age);
        },
        data(){
            return {}
        }
    }
</script>
<style>
</style>