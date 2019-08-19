<template>
  <div id="app">
    <Search/>
    <div class="movies">
      <Movie v-for="movie in movies"
    :key="movie.id" :title="movie.title"
    :poster="movie.poster_path" :overview="movie.overview"
    :release="movie.release_date" :vote_average="movie.vote_average"
    />
     </div>
  </div>
</template>

<script>
import Movie from "./components/Movie.vue";
import Search from "./components/Search.vue"

export default {
  name: "app",
  components: {
    Search,
    Movie
  },
  data(){
    return{
      movies: []
    }
  },
  created(){
      const data = fetch('https://api.themoviedb.org/3/discover/movie?primary_release_year=2019/api_key=9084eae9f770e006ebcba95dbd474e28')
      data.then(response=>response.json()).then(data=>this.movies = data.results)
  }
};
</script>

<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.movies {
  display:flex;
  width: 100%;
  flex-wrap: wrap;
  align-items: flex-start;
}
</style>
