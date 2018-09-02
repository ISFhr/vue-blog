<template>
  <div v-theme:column="narrow" id="show-blogs">
      <h1>博客总览</h1>
      <input type="text" v-model="search" placeholder="搜索">
      <div v-bind:key="index" v-for="(blog,index) in filteredBlogs" class="single-blog">
        <router-link v-bind:to="'/blog/' + blog.id">
            <h2 v-rainbow>
                {{blog.title | to-uppercase}}
            </h2>
        </router-link>
        <article>
                {{blog.body | snippet}}
        </article>
      </div>


  </div>
</template>

<script>



export default {
  name: 'show-blogs',
  data(){
      return{
          blogs:[],
          search:"",
          narrow: ""
      }
  },
  created() {
      this.$http.get('https://jsonplaceholder.typicode.com/posts')//请求数据
      .then(function(data){
        //   console.log(data)
        this.blogs = data.body.slice(0,10);
        // console.log(this.blogs)
      })

  },
  computed:{
      filteredBlogs:function(){
          return this.blogs.filter((blog) =>{
              return blog.title.match(this.search);
          })
      }
  },
//局部local定义API （两种方法）
//   filters:{
//       "to-uppercase":function(value){
//           return value.toUpperCase();
//       }
//   }
//   filters:{
//       toUpperCase(value){
//           return value.toUpperCase();
//     }
//   },

//local 定义标题颜色
  directives:{
      'rainbow':{
          bind(el,binding,vnode){
                el.style.color = "#" + Math.random().toString(16).slice(2,8);
          }
      }
  }
}
</script>

<style>
    #show-blogs{
        max-width:800px;
        margin:0 auto;
    }
    .single-blog{
        padding: 20px;
        margin:20px 0;
        box-sizing: border-box;
        background: #eee;
        border: 1px dotted #aaa;
    }
    #show-blogs a{
        color:#444;
        text-decoration: none;
    }
    input[type="text"]{
        padding: 8px;
        width:100%;
        box-sizing: border-box;
    }

</style>