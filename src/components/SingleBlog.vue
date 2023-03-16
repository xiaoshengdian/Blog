<template>
  <div id="sinle-blog">
    <h1>{{blog.title}}</h1>
    <article>{{blog.content}}</article>
    <p>作者：{{author}}</p>
    <p>分类：</p>
    <ul>
        <li v-for="category in blog.categories">
            {{category}}
        </li>
    </ul>
    <button @click="del()">删除</button>
    <router-link :to="'/edit/'+id">编辑</router-link>
  </div>
</template>

<script>
export default {
    name:"single-blog",
    data(){
        return{
            id:this.$route.params.id,
            blog:{}
        }
    },
    created(){
        this.$http.get('https://boke-fb75a-default-rtdb.firebaseio.com/posts/' + this.id +".json")
        .then(function(data){
            console.log(data);
            return data.json();
            // this.blog = data.body;
        })
        .then(function(data){
            this.blog=data;
        })
    },
    methods:{
        del(){
            this.$http.delete("https://boke-fb75a-default-rtdb.firebaseio.com/posts/"+ this.id +".json")
            .then(response =>{
                this.$http.push({path:'/'})
            })
        }
    }
}
</script>

<style>
#sinle-blog{
    max-width: 960px;
    margin: 0 auto;
    padding: 20px;
    background: #eee;
    border: 1px dotted #aaa;
}
</style>