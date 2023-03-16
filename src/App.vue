<template>
  <div id="app">
    
    <!-- <AddBlog/> -->
    <!-- <show-blogs></show-blogs> -->
   
    <HelloWorld/>
    <router-view></router-view>
  </div>
</template>

<script>
import AddBlog from './components/AddBlog'
import ShowBlogs from './components/ShowBlogs'
import HelloWorld from './components/HelloWorld'

export default {
  name: 'App',
  components: {
    AddBlog,ShowBlogs,HelloWorld
    
  }
}
</script>

<style>
#app {

}
</style>
