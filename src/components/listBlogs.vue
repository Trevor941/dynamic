<template>
  <div id="show-blogs" v-theme:column="'narrow'">
<h1>List of all blogs</h1>
<input type="text" v-model="search" placeholder="search blogs">
<div class="single-blog" v-for="blog in filteredBlogs" v-bind:key="blog">
 <h3 v-rainbow>{{blog.title | toUppercase}} </h3>
 
</div>
</div>
</template>

<script>


export default {
   
  name: 'app',
  data () {
    return {
      blogs: [],
      search:''
    }
  },
 
  methods:{
    
  },
  computed:{
        filteredBlogs: function(){
            return this.blogs.filter((blog)=>{
             return blog.title.match(this.search);
           } )
         }
    },
  created(){
       this.$http.get("http://jsonplaceholder.typicode.com/posts").then(function(data){
            this.blogs = data.body.slice(0, 10);
          })
  },
 
  filters:{
    toUppercase(value){
     return value.toUpperCase();
    },
    snippet(value){
     return `${value.slice(0, 100)} ...`; 
    }
  },
  directives:{
    rainbow:{
      bind(el, binding, vnode){
    el.style.color = '#' + Math.random().toString().slice(2,8);
    }
    }
  },
 
  
}
</script>

<style>
#show-blogs{
    max-width: 800px;
    margin: 0 auto;
}
.single-blog{
    padding: 20px;
    margin: 20px 0;
    box-sizing: border-box;
    background: #eee;
}

</style>
