<template>
  <div id="app">
    <Search @search="update($event)" />
      <div class="numRes">Showing 20 of {{total_results}}</div>
    <div class="movies" >
      <template v-if="!searchData">
      <Movie
        v-for="movie in initalData.results"
        :key="movie.id"
        :title="movie.title"
        :poster="movie.poster_path"
        :overview="movie.overview"
        :release="movie.release_date"
        :vote_average="movie.vote_average"
      /> 
      </template>
      <template v-else>
        <Movie
        v-for="movie in searchData.results"
        :key="movie.id"
        :title="movie.title"
        :poster="movie.poster_path"
        :overview="movie.overview"
        :release="movie.release_date"
        :vote_average="movie.vote_average"
      />
      </template>
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
      initialData: [],
      page: 1,
      searchData: [],
      total_results: 0,
    };
  },
  created() {
    this.getData()
  },
  methods: {
    async getData() {
      const data = await fetch(
      `https://api.themoviedb.org/3/discover/movie?primary_release_year=2019&page=1&api_key=9084eae9f770e006ebcba95dbd474e28`
    ).then(response => response.json()).then(data => {
      this.initalData = data
      this.total_results = data.total_results
    })
    },
    pagi(page) {
        return this.page;
      },
    update(data) {
      this.searchData.results = data
      this.total_results = data.total_results
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
  color: #e2e2e2;
  margin-top: 60px;
}
.movies {
  display: flex;
  width: 100%;
  flex-wrap: wrap;
  align-items: flex-start;
  justify-content: space-around;
}
.numRes {
  margin: auto;
  font-size: 1.25rem;
}
</style>
