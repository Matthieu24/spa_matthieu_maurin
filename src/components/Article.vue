<template>
  <div class="article">
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Article',
  props: {
  },
  data () {
    return {
      articles:[],   
    }
  },

  computed: {},
  created() {
    axios.get("https://jsonplaceholder.typicode.com/posts")
      .then(response => {
          this.articles = response.data;
          console.log(this.articles);
          console.log(response.data);
      })
      .catch(function (error) {
        console.log(error);
      });
      test();
  },
  methods:{
    test(){
      console.log('ok')
    }
  },
  mouthed(){

    
  },
}


</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
