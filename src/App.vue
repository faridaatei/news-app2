<template>

  <div class="container">

  <input type="search" v-model="search" id="site-search" name="q"
               placeholder="type to search..."
               aria-label="Search through site content" />

        <button v-on:click="loadNews" type="button">Search</button>
       
  

<div class="content" v-for = "article in news">

<img  v-if="article.urlToImage":src="article.urlToImage" alt="">

<h3>
  {{article.title}}
</h3>
<h4>{{article.author}}</h4>

<p>{{article.description}}</p>

<button class="button button-outline">Outlined Button</button>
<p v-if="loading">loading ........</p>
<div class="lds-roller" v-if="loading"><div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div></div>


</div>


   

    

  </div>

</template>

<script>

const baseurl="https://newsapi.org/v2/";
const apiKey ="7716db983a0d4b429e6fdcea39ffff9d";
const endpoint ="/everything";



import axios from 'axios'

const data = {
  news:[],
  search:  '',
  loading:false
  
  
  
  
}


export default {
  data: function() {
    return data
  },
  created(){
 this.loadNews();
  },
  methods:{
    loadNews() {

      if(this.search.length < 1) {
        return
      }
      this.loading =true;
      this.news= [];

      let url =baseurl 
      +endpoint
      +'?q=' +this.search
      + '&apiKey=' + apiKey;

 axios.get(url).then(function(response) {
    console.log(response.data.articles)
    data.news = response.data.articles
  }).catch(function(error){
  consiole.log(error.message)
  })
  
  }
  }
}
</script>