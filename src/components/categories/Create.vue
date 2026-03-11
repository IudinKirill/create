<script>

    export default {
        data(){
            return {
                name: '',
            }
        },
        methods: {
        createCategory(){
            if (!this.name.trim()) {
                alert('Введите название категории');
                return;
            }
            this.$emit('createCategory', this.name);
            this.name = '';
        }
    }
    }
</script>



<template>
    <div>
        <input type="text" v-model="name" placeholder="Name">
        <button @click="createCategory()">Create</button>
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
    input{
       width: 100%; 
       text-align: center;
    }
</style>
