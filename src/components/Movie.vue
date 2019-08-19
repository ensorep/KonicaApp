<template>
<div class="movie">
    <div class="movie-title">{{title}}</div>
    <img class="movie_poster" :src="imgpath + poster"  />
    <div class="movie-release">{{release}}</div>
    <div class="movie-overview">{{overview}}</div>
    <div class="movie-voteAvg">Average rating: {{vote_average}} / 10</div>
</div>
</template>

<script>
export default {
    name: 'Movie',
    props: {
        title: String,
        overview: String,
        release: String,
        vote_average: Number,
        poster: String,
    },
    computed:{
       
    },
    data() {
        return {
            imgpath:`https://image.tmdb.org/t/p/w500`
        }
    }
}
</script>

<style lang="scss" scoped>
 .movie {
     display: flex;
     flex: 1;
     flex-direction: column;
     justify-content: space-evenly;
     margin: 1rem;
     max-width: 360px;
    &_poster {
        height: 400px;
    }
    &-overview {
        margin: auto;
        text-align: left;
    }
    &-title {
        margin: 1rem 0;
    }
    &-release {
        margin: 1rem 0;
    }
    &-voteAvg {
        margin: 1rem;
    }
 }
</style>