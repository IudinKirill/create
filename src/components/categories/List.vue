<script>
import PaginateCategory from '@/components/categories/Paginate.vue'
import ItemCategory from '@/components/categories/Item.vue'
import CreateCategory from '@/components/categories/Create.vue'
    export default{
        components:{ ItemCategory, PaginateCategory, CreateCategory },
        data(){
            return{
                categories: [],
                links: [],
                from: 1,
                link: 'http://srvydy.ru/api/categories'
            }
        },
        methods:{
            async loadCategories(link){
                if(link){
                    this.link = link
                }
                const response = await fetch(this.link)
                this.categories = await response.json()
                this.links = this.categories.meta.links
                 this.from = this.categories.meta.from
            },
            async deleteCategory(id){
                const response = await fetch('http://srvydy.ru/api/categories/'+id, {
                    "method": "DELETE",                
                    "headers": {
                        "Accept": "application/json",
                        "Content-Type": "application/json"
                    }
                    }

                )
                if(response.status == '204'){
                   this.loadCategories() 
                }
                if(response.status == '404'){
                    this.loadCategories()
                    alert('Такой категории нет')
                }
                if(response.status == '500'){
                    this.loadCategories()
                    alert('Сервер не отвечает')
                }
            },
            async addCategory(name) { 
            const response = await fetch(this.link, {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                    'Accept': 'application/json'
                },
                body: JSON.stringify({ name })
            })

            if (response.ok) {
                this.loadCategories() 
            } else {
        const error = await response.json().catch(() => ({}))
        console.log('Ошибка: ' + (error.message || 'Не удалось создать'))
    }
        }
        },
        mounted(){
            this.loadCategories()
        }
    }
</script>



<template>
        <h2>Categories</h2>
        <PaginateCategory @loadPage="loadCategories" :links/>
        <CreateCategory @createCategory="addCategory"/>
        <ul>
            <li v-for="(category,index) in categories.data" :key="category.id">
                <ItemCategory @deleteCategory="deleteCategory" :category="category" :index="index" :from="from"/>
            </li>
        </ul>
</template>



<style scoped>
    h2{
        text-align: center;
    }
    ul{
        margin: 0 auto;
        width: 50%;
        list-style-type: none;
    }
    li{
        cursor:pointer;
        transition: 400ms;
    }
    li:hover{
        transform:scale(1.03)
    }    
    li:nth-child(2n-1){
        background-color: lightgray;
    }
</style>
