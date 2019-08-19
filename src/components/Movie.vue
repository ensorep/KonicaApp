<template>
<div class="movie">
    <img class="movie_poster" :src="imgpath + poster"  />
    <div class="movie_info">
        <div class="movie_info-title">{{title}}</div>
        <div class="movie_info-release">{{release}}</div>
        <div class="movie_info-overview">{{overview}}</div>
        <div class="movie_info-voteAvg">Average rating: {{vote_average}} / 10</div>
    </div>
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
    background-color: #e2e2e2;
    position: relative;
    border-radius: 3px;
    display: flex;
    flex: 1;
    flex-direction: column;
    justify-content: space-evenly;
    margin: 1rem;
    max-width: 330px;
  &_poster {
    height: 350px;
  }
    &_info {
      display: flex;
      flex-direction: column;
      color: #e2e2e2;
      position: absolute;
      top: 0;
      bottom: 0;
      left: 0;
      right: 0;
      background-color: rgba(0,0,0,0.6);
      opacity: 0;

      &:hover {
        cursor: pointer;
        opacity: 1;
      }

      &-overview {
        text-align: left;
        margin: 1rem;
      }
      &-title {
        margin: 1rem .5rem;
      }
      &-release {
        margin: 1rem 0;
      }
      &-voteAvg {
        margin: 1rem;
      }
    }
 }
</style>