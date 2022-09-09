<template>
  <div class="article">
    <h1>Article numéro : {{article.id}} </h1>
    
    <div class = "ArticleLogo" v-bind:style="{'background-color': randomColor()}">
      <p><router-link :to="{ name: 'home'}" style="text-decoration:none; color:black" class="link" ><span>{{firstLetter}}</span></router-link></p>

    </div>
  
    <h3 style="display:inline-block">{{article.title}}</h3>
    <p style="width:100%;">{{article.body}}</p>
    <hr>
    <div id="comment" style="margin-top:2rem;">
      <h3><u>Commentaires</u></h3>
      <div v-for="comment in comments" :key="comment.id" >
        <p style="font-weight:bold">{{comment.name}}</p> 
       <p style="color: blue;"><u>{{comment.email}}</u></p> 
        <p style="margin-bottom:5rem;">{{comment.body}}</p>
      </div>
    </div>
   </div>
   
    


</template>

<script>
alert('message pour le prof : pour revenir en arrière cliquer sur le rond coloré')
// @ is an alias to /src
import Article from '@/components/Article.vue'

import axios from 'axios'

export default {
  name: 'ArticleView',
  components: {
    Article
  },

    data (){
    return{
        id: this.$route.params.id,
        article:[],
        comments: [],
        firstLetter:'',
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
    this.getArticle();
    this.getComments();
  },

  methods:{
    getArticle(){
      axios.get(`https://jsonplaceholder.typicode.com/posts/${this.id}`)
      .then(response => {
          this.article = response.data;
          console.log(this.article.title);
          
          this.firstLetter = this.getFirstLetter(this.article.title);
      })
      .catch(function (error) {
        console.log(error);
      });
    },

    getComments(){
      axios.get(`https://jsonplaceholder.typicode.com/posts/${this.id}/comments`)
      .then(response => {
          this.comments = response.data;
          console.log(this.comments);
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

<style>
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

.ArticleLogo:hover .link span{
 display: none;
}

.ArticleLogo:hover .link:before{
   content: '←';
}
</style>