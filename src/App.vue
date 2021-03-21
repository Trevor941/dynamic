<template>
  <div >
    <appheader></appheader>
<router-view></router-view>
    </div>
</template>

<script>
import showBlog from './components/showBlogs.vue'
import listBlogs from './components/listBlogs.vue'
import appheader from './components/header.vue'
export default {
  components:{
    'show-blogs': showBlog,
    'list-blogs': listBlogs,
    'appheader': appheader
  },
  name: 'app',
  data () {
    return {
      
    }
  }
}
</script>

<style>


</style>
