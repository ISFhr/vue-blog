<template>
  <div id="add-blog">
   <h2>添加博客</h2>
   <form v-if="!submmited">
       <label for="id">博客标题</label>
       <input id="id" type="text" v-model="blog.title" required/>
       <!-- v-model绑定下面的blog：title -->
       <!-- required 属性规定必需在提交表单之前填写输入字段
       v-model 本质上是语法糖。它负责监听用户的输入事件以更新数据，并对一些极端场景进行一些特殊处理。 -->



       <label>博客内容</label>
       <textarea v-model="blog.content"></textarea>

       <div id="checkboxes">
           <label>Vue.js</label>
           <input type="checkbox" value="Vue.js" v-model="blog.categories">
           <label>Node.js</label>
           <input type="checkbox" value="Node.js" v-model="blog.categories">
           <label>React.js</label>
           <input type="checkbox" value="React.js" v-model="blog.categories">
           <label>Angular4</label>
           <input type="checkbox" value="Angular4" v-model="blog.categories">
           <br>

        <label>作者：</label>
           <select v-model="blog.author">
               <option v-bind:key="index" v-for="(author, index) in authors">
                   {{author}}
               </option>
           </select>
        <!-- <select> 元素用来创建下拉列表。
        <select> 元素中的 <option> 标签定义了列表中的可用选项。 -->
        <button v-on:click.prevent="post">添加博客</button>
        <!-- v-on:click.prevent 提交时间不再重载页面 -->
       </div>
   </form>

   <div v-if="submmited">
       <h3>您的博客发布成功！</h3>
   </div>
   <div id="preview">
       <h3>博客总览</h3>
       <p>博客标题:{{blog.title}}</p>
       <p>博客内容:</p>
       <p>{{blog.content}}</p>
       <p>博客分类:</p>
       <ul>
           <li v-for="category in blog.categories" v-bind:key="category">
               {{category}}
           </li>
       </ul>
        <p>作者:{{blog.author}}</p>
   </div>
  </div>
</template>

<script>
export default {
    //http://jsonplaceholder.typicode.com
    //http://jsonplaceholder.typicode.com/posts
  name: 'add-blog',
  data () {
    return {
        blog:{
            title:"",
            content:"",
            categories:[],
            author:"",

        },
        authors:["Kucy","Annie","Henry"],
        submmited: false
    }
  },
  methods:{ 
      post() {
          this.$http.post("http://jsonplaceholder.typicode.com/posts", {
              title:this.blog.title,
              body:this.blog.content,
              userId:1,
           }).then(function(data) {
               console.log(this.blog.categories);
                this.submmited = true;
           })
      }
    //   Vue与后端数据交互：需要引入库：vue-resource
    // 使用this.$http.get('请求地址')来发送请求,获取json中的数据，后面可加参数。
    // then()方法异步执行，就是当then()前面的方法执行完之后在执行then()里面的方法，这样就不会发生获取不到数据的问题。
    

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#add-blog *{
    box-sizing: border-box;   
}
#add-blog{
    margin: 20px auto;
    max-width: 600px;
    padding: 20px;
}
label{
    display: block;
    margin: 20px 0 10px;
}
input[type="text"],textarea,select{
    display: block;
    width:100%;
    padding: 8px;
}
textarea{
    height: 200px;
}
#checkboxes label{
    display: inline-block;
    margin-top: 0;
}
#checkboxes input{
    display: inline-block;
    margin-right: 10px;
}
button{
    display: block;
    margin: 20px 0;
    background:dimgrey;
    color:#fff;
    border: 0;
    padding: 14px;
    font-size: 18px;
    border-radius: 4px;
    cursor: pointer;
}
#preview{
    padding: 10px 20px;
    border: 1px dotted grey;
    margin: 30px 0;
}
h3{
    margin-top: 10px;
}


</style>
