<template>
  <div class="home">
    <div v-for="article in articles" :key="article.id">
   {{article.title}}
    </div>
 
  </div>
</template>

<script>
import axios from 'axios'

// let articles = [];
// axios.get("https://jsonplaceholder.typicode.com/posts")
//       .then(response => {
//           articles = response.data;
//           console.log(articles);
//       })
//       .catch(function (error) {
//         console.log(error);
//       });

export default {
  name: 'Home',
  data (){
    return{
        articles:[{id:'1', title:'aer'}],
    }
  },

  created(){
    this.getArticles();
  },

  mounted(){
    this.getArticles();
  },

  methods:{
    getArticles(){
      axios.get("https://jsonplaceholder.typicode.com/posts")
      .then(response => {
          this.articles = response.data;
          console.log(this.articles);
      })
      .catch(function (error) {
        console.log(error);
      });
    }
  },
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
