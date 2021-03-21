<template>
  <div id="add-blog">
    <h2>Add a New Blog Post</h2> 
    <form action="" v-if="!submitted">
    <label for="">Blog Title</label>
       <input type="text" v-model="blog.title" required > 
       <label for="">Blog Content</label>
       <textarea v-model="blog.content"> </textarea>
       <h3>Categories</h3>
       <div id="checkboxes">
     <label for="">Cheese</label>
       <input type="checkbox"  name="" v-model="blog.categories" value="cheese">
       <label for="">Peanut butter</label>
       <input type="checkbox"  name="" v-model="blog.categories" value="peanut butter">
       <label for="">Pine</label>
       <input type="checkbox"  name="" v-model="blog.categories" value="pine">
       <label for="">Chilli</label>
       <input type="checkbox"  name="" v-model="blog.categories" value="chilli">
       </div>
       <label for="">Authors</label>
      <select name="" id="" v-model="blog.author">
        <option v-for="author in authors" v-bind:key="author">{{author}}</option>
      </select><br>
      <button v-on:click.prevent="post">Add Blog</button>
       
    </form>
    <div v-if="submitted">
       <p>Thanks for submitting the form</p>
       </div>
    <div id="preview">
      <h3>Preview Blog</h3>
      <p><b>Blog Title:</b>{{blog.title}}</p>
      <p><b>Blog Content:</b></p>
      <p>{{blog.content}}</p>
      <p>Categories</p>
      <ul>
        <li v-for="category in blog.categories" v-bind:key="category">{{category}}</li>
      </ul>
      <label for=""><b>authors:</b></label>
      <p>{{blog.author}}</p>
      
    </div>
  </div>
</template>

<script>

export default {
 
  name: 'app',
  data () {
    return {
      blog:{
          title:"",
          content:"",
          categories: [],
          author: ""
      },
      authors: ['Trevor', 'Tshuma', 'Bigboy'],
       submitted: false
    }
   
  },
  methods: {
    post: function(){
      this.$http.post('https://another1-b7b07-default-rtdb.firebaseio.com/posts.json', this.blog).then(function(data){
        console.log(data);
        this.submitted = true;
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
    margin: 20px auto;
    max-width: 500px;
}
label{
    display: block;
    margin: 20px 0 10px;
}
input[type="text"], textarea{
    display: block;
    width: 100%;
    padding: 8px;
}
#preview{
    padding: 10px 20px;
    border: 1px dotted #ccc;
    margin: 30px 0;
}
h3{
    margin-top: 10px;
}
#checkboxes input{
  display: inline-block;
  margin-right: 10px;
}
#checkboxes label{
  display: inline-block;
}
</style>
