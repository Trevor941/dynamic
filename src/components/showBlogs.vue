<template>
  <div id="show-blogs" v-theme:column="'narrow'">
<h1>List of all blogs</h1>
<input type="text" v-model="search" placeholder="search blogs">
<div class="single-blog" v-for="blog in filteredBlogs" v-bind:key="blog">
<router-link v-bind:to="'blog/' + blog.id"><h3 v-rainbow>{{blog.title | toUppercase}} </h3></router-link>
 <p>{{blog.content | snippet}}</p>
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
  created(){
       this.$http.get("https://another1-b7b07-default-rtdb.firebaseio.com/posts.json").then(function(data){
            return data.json();
          }).then(function(data){
            var blogsArray = [];
            for (let key in data){
              data[key].id = key
              blogsArray.push(data[key]);
            }
            this.blogs = blogsArray;
          })
  },
  
      computed:{
        filteredBlogs: function(){
            return this.blogs.filter((blog)=>{
             return blog.title.match(this.search);
           } )
         }
    }
  ,
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
  }
  
  
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
