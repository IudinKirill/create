<script>
    export default{
        props: ['category', 'index', 'from'],
        methods:{
            deleteCategory(id){
                this.$emit('deleteCategory', id)
            }
        }
    }
</script>



<template>
    <div>
        <span>{{ from*1 + index }}</span>
        <p>{{ category.name }}</p>
        <button @click="deleteCategory(category.id)">Delete</button> 
    </div>
    
</template>



<style scoped>
    button{
        padding: 6px 12px;
        border: 1px solid red;
        background-color: red;
        border-radius: 4px;
        color: white;
        font-size: 16px;
        transition: 400ms;
        cursor:pointer;
    }
    button:hover{
        color:red;
        background-color: white;
    }
    div{
        padding: 6px 1vw;
        display:grid;
        grid-template-columns: auto 1fr auto;
        align-items: center;
        column-gap: 2vw;
    }
    p{
    overflow-wrap: break-word;
    word-break: break-word;
    }
</style>
