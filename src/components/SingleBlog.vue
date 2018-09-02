<template>
    <div id="single-blog">
        <h1>{{blog.title}}</h1>
        <article>{{blog.body}}</article>
        <p>作者：{{blog.author}}</p>
        <p>分类：</p>
        <ul>
            <li v-bind:key="index" v-for="(category,index) in blog.catebories">
                {{category}}
            </li>
        </ul>

        <!-- 删除功能
        <button @click="deleteSingleBlog()">删除</button> -->

        <!-- 编辑功能 -->
        <!-- <router-link to="'/edit/ + id'">编辑</router-link> -->


    </div>
</template>

<script>
    export default{
        name:"single-blog",
        data(){
            return{
                id:this.$route.params.id,
                blog:{}
            }
        },
        created(){
            this.$http.get('https://jsonplaceholder.typicode.com/posts/' + this.id)
            .then(function(data){
                // console.log(data.body.catebories);
                this.blog = data.body;
            })
        }
        

        //删除功能
        //     deleteSingleBlog(){
        //         this.$http.delete('https://jsonplaceholder.typicode.com/posts/' + this.id)
        //         .then(response =>{
        //             this.$router.push({path:'/'})
        //         })

        }

</script>

<style>
    #single-blog{
        max-width: 960px;
        margin: 0 auto;
        padding: 20px;
        background:#eee;
        border: 1px dotted #aaa
    }

</style>

