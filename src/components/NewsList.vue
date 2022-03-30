

<template>
    <form @submit.prevent="searchNews" class="d-flex flex-column justify-content-center">
        <div class="input-group mx-sm-3 mb-2">
            <label class="visually-hidden" for="search">Search
            </label>
            <input type="search" name="search" v-model="searchTerm" id="search" class="form-control mb-2 mr-sm-2" placeholder="Enter search term here" />
            <button class="btn btn-primary mb-2">Search</button>
        </div>
        <p>You are searching for {{ searchTerm }}</p>
    </form>

    <div class="grid-container">
        <div v-for="article in articles" class="card shadow-sm">
            <img :src=article.urlToImage class="card-image-top" alt="article image"/>
            <div class="card-body">
                <h5 class="card-title">{{article.title}}</h5>
                <p class="card-text"> {{ article.description }} </p>
            </div>
        </div>
    </div>

    
</template>

<script>
export default {
    data() {
        return {
            articles: [],
            searchTerm: ''
        };
    },

    methods:{
        searchNews() {
            let self = this;

            fetch('https://newsapi.org/v2/everything?q='+ self.searchTerm + '&language=en',{
                headers:{
                    'Authorization': `Bearer ${import.meta.env.VITE_NEWSAPI_TOKEN}`,
                }
            })
                .then(function(response){
                return response.json();
            })
                .then(function(data){
                console.log(data);
                self.articles = data.articles;
            });
        },

        
    } 


};


</script>

<style>
.grid-container{
  display: grid;
  grid-template-columns: auto auto auto;
  gap: 20px 20px;
  width:100% ;
  margin-top: 30px;
}

.card{
   max-width: 350px;
}
h5{
    text-align: left;
}
.card-body p{
    text-align: justify;
}

</style>
