

<template>
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
            articles: []
        };
    },

    created() {
        let self = this;

        fetch('https://newsapi.org/v2/top-headlines?country=us',{
            headers: {
                'Authorization': `Bearer ${import.meta.env.VITE_NEWSAPI_TOKEN}`
            }
        })
            .then(function(response){
                return response.json();
            })
            .then(function(data){
                console.log(data);
                self.articles = data.articles;
            });
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
