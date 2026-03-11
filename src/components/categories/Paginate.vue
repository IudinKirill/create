<script>
    export default{
        props:['links'],
        methods:{
            loadPage(link){
                this.$emit('loadPage',link)
            }
        }
    }
</script>



<template>
    <div>
        <button v-for="link in links" :disabled="link.active" v-html="link.label" @click="
        loadPage(link.url)"></button>
    </div>

</template>



<style scoped>
    div{
        width: 50%;
        margin: 0 auto;
        display: flex;
        justify-content: space-between;
    }
    button{
        width: 100%;
        padding: 4px 0;
    }
</style>