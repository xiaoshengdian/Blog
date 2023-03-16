<template>
  <div id="add-blog">
    <h2>添加博客</h2>
    <form v-if="!submmited">
        <label>博客标题</label>
        <input type="text" v-model="blog.title" required />

        <label>博客内容</label>
        <textarea v-model="blog.content"></textarea>
        <div id="checkboxes">
            <label>vue.js</label>
            <input type="checkbox" value="vue.js" v-model="blog.categories">
            <label>Node.js</label>
            <input type="checkbox" value="Node.js" v-model="blog.categories">
            <label>React.js</label>
            <input type="checkbox" value="React.js" v-model="blog.categories">
            <label>Angular4</label>
            <input type="checkbox" value="Angular4" v-model="blog.categories">
        </div>
        <label>作者</label>
        <select v-model="blog.author">
            <option v-for="author in authors">
                {{author}}
                </option>
        </select>
        <button v-on:click.prevent="post">添加博客</button>
    </form>
    <div v-if="submmited">
        <h2>博客添加成功</h2>
    </div>
     
     <!-- 显示 -->
    <div id="preview">
        <h3>博客总览</h3>
        <p>博客标题：{{blog.title}}</p>
        <p>博客内容：</p>
        <p>{{blog.content}}</p>
        <p>博客分类：</p>
        <ul>
            <li v-for="category in blog.categories">  <!-- 不碍事，vue的插件vutur语法检查报错，语法没有错误，但是检查语法的时候没有写key就会报错 -->
                {{category}}
            </li>
        </ul>
        <p>作者：{{blog.author}}</p>
    </div>
  </div>
</template>

<script>
export default {
      name:'hadd-blog',
      data(){
        return{
            blog:{
                title:"",
                content:"",
                categories:[],
                author:""
            },
            authors:["zhou","kang","fufu"],
            submmited:false


        }
      },
      methods:{
        post:function(){
            this.$http.post("https://boke-fb75a-default-rtdb.firebaseio.com/posts.json",this.blog)
            .then(function(data){
                console.log(data);
                this.submmited=true;
            });
        }
      }
}
</script>

<style>

#add-blog *{
    box-sizing: border-box;
}

#add-blog{
    margin:5px auto;
    max-width: 600px;
    padding: 5px;
}

label{
    display: block;
    margin: 20px auto;
}

input[type="text"],textarea,select{
    display: block;
    width: 100%;
    padding: 8px;
}

#checkboxes label{
    display: inline-block;
    margin-top: 2px;
    margin-left: 10px;
}
#checkboxes input{
    display: inline-block;
    margin-right: 56px;
}

textarea{
    height: 200px;
}

button{
    display: block;
    margin: 20px 0;
    background: crimson;
    color: #fff;
    border: 0;
    padding:12px;
    border-radius: 4px;
    font-size: 16px;
    cursor: pointer;
}

#preview{
    padding: 10px 20px;
    border: 1px dotted #ccc;
}
h3{
    margin-top: 10px;
}
</style>
