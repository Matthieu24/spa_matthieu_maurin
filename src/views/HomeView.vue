<template>
  <div class="home">
    <h1>Matthieu Maurin TP SPA</h1>
    <!-- <img alt="Vue logo" src="../assets/logo.png"> -->
   <div v-for="article in articles" :key="article.id">
    <div class = "ArticleLogo" v-bind:style="{'background-color': randomColor()}"><p>{{getFirstLetter(article.title)}}</p>
    </div>
    <router-link :to="{ name: 'article', params: { id: article.id }}">{{article.title}}</router-link>

   <hr style="width:70%; margin-bottom:1.5rem; margin-top:1.5rem;">
    </div>
  </div>
  
</template>

<script>
// @ is an alias to /src
import Home from '@/components/Home.vue'

import axios from 'axios'

export default {
  name: 'HomeView',
  components: {
    Home
  },
    data (){
    return{
        articles:[],
        colors:['#FF6633', '#FFB399', '#FF33FF', '#FFFF99', '#00B3E6', 
                '#E6B333', '#3366E6', '#999966', '#99FF99', '#B34D4D',
                '#80B300', '#809900', '#E6B3B3', '#6680B3', '#66991A', 
                '#FF99E6', '#CCFF1A', '#FF1A66', '#E6331A', '#33FFCC',
                '#66994D', '#B366CC', '#4D8000', '#B33300', '#CC80CC', 
                '#66664D', '#991AFF', '#E666FF', '#4DB3FF', '#1AB399',
                '#E666B3', '#33991A', '#CC9999', '#B3B31A', '#00E680', 
                '#4D8066', '#809980', '#E6FF80', '#1AFF33', '#999933',
                '#FF3380', '#CCCC00', '#66E64D', '#4D80CC', '#9900B3', 
                '#E64D66', '#4DB380', '#FF4D4D', '#99E6E6', '#6666FF'],
    }
  },
   created(){
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
    },
    randomColor(){
      const color = Math.floor(Math.random() * this.colors.length);
      return this.colors[color];
    },
    getFirstLetter(title){
      return title.substr(0,1).toUpperCase()
    }
  },
}

</script>

<style scoped>

.ArticleLogo{
  text-align: center;
  display: inline-block;
  width: 32px; 
  height: 32px;
  border-radius: 50%;
  margin-right: 1rem;
}
.ArticleLogo p{
  margin-top: 0.5rem;
}
</style>
