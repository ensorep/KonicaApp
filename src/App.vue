<template>
  <div id="app">
    <Search />
      <div class="numRes">showing 20 of {{data.total_results}}</div>
    <div class="movies">
      <Movie
        v-for="movie in data.results"
        :key="movie.id"
        :title="movie.title"
        :poster="movie.poster_path"
        :overview="movie.overview"
        :release="movie.release_date"
        :vote_average="movie.vote_average"
      />
    </div>
    <div class="pagi">
      <span class="pagi_prev" @click="pagi(page--)">&lt;</span>
      Page {{page}} of {{data.total_pages}}
      <span class="pagi_next" @click="pagi(page++)">&gt;</span>
    </div>
  </div>
</template>

<script>
import Movie from "./components/Movie.vue";
import Search from "./components/Search.vue";

export default {
  name: "app",
  components: {
    Search,
    Movie
  },
  data() {
    return {
      data: [],
      page: 1,
      pagi: page => {
        return page;
        // this.created()
      }
    };
  },
  created() {
    const data = fetch(
      `https://api.themoviedb.org/3/discover/movie?primary_release_year=2019&page=${this.page}&api_key=9084eae9f770e006ebcba95dbd474e28`
    );
    data.then(response => response.json()).then(data => (this.data = data)).catch(() => {throw Error});
  }
};
</script>

<style lang="scss">

html,body  {
  background-color: #b375e4;
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.movies {
  display: flex;
  width: 100%;
  flex-wrap: wrap;
  align-items: flex-start;
  justify-content: space-around;

}
</style>
