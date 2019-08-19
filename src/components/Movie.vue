<template>
<div class="movie">
    <img v-if="poster" class="movie_poster" :src="`https://image.tmdb.org/t/p/w500${poster}`" :alt="`${title} poster image`"  />
    <div v-else class="movie_no-poster">No Image Available</div>
    <div class="movie_info">
        <div class="movie_info-title">{{title}}</div>
        <div class="movie_info-release">Release date: {{release}}</div>
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
}
</script>

<style lang="scss" scoped>
 .movie {
    position: relative;
    display: flex;
    flex: 1;
    flex-direction: column;
    justify-content: space-evenly;
    margin: 1rem;
    min-width: 250px;
    max-width: 330px;
    min-height: 350px;
  &_poster {
    height: 350px;
    border-radius: 5px;
  }
  &_no-poster{
    text-align: center;
    height: 350px;
    min-width:250px;
    max-width: 330px;
    color: #000;
    background-color:#61544b;
    border-radius: 5px;
    font-size: 1.5rem;
  }
    &_info {
      border-radius: 5px;
      display: flex;
      flex-direction: column;
      position: absolute;
      top: 0;
      bottom: 0;
      left: 0;
      right: 0;
      background-color: rgba(0,0,0,0.65);
      opacity: 0;

      &:hover {
        cursor: pointer;
        opacity: 1;
      }

      &-overview {
        text-align: left;
        margin: 1rem;
        height: 60%;
        overflow: auto;
        user-select: none;
      }
      &-title {
        margin: 1rem .5rem;
        font-size: 1.25rem;
      }
      &-voteAvg {
        margin: 1rem;
      }
    }
 }
</style>