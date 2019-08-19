<template>
  <div id="app">
    <Search />
      <div class="numRes">showing 20 of {{data.total_results}}</div>
    <div @search="this.update($event)" class="movies">
      <Movie
        v-for="movie in data"
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
      searchy: []
    };
  },
  created() {
    this.getData()
  },
  methods: {
    async getData() {
      const data = await fetch(
      `https://api.themoviedb.org/3/discover/movie?primary_release_year=2019&page=1&api_key=9084eae9f770e006ebcba95dbd474e28`
    ).then(response => response.json()).then(data => this.data = data.results)
    },
    pagi(page) {
        return this.page;
        // this.created()
      },
    update(event) {
      console.log('in update on app')
      this.searchy = event
    }
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
