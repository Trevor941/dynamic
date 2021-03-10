<template>
  <div >
<route-view></route-view>
    </div>
</template>

<script>
import showBlog from './components/showBlogs.vue'
import listBlogs from './components/listBlogs.vue'
export default {
  components:{
    'show-blogs': showBlog,
    'list-blogs': listBlogs
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
