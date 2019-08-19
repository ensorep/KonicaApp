<template>
  <div id="app"> 
    <img alt="Vue logo" src="./assets/logo.png">
    <Search @search="update($event)" />
      <div v-if="total_pages > 1" class="numRes">Showing 20 of {{total_results}}</div>
      <div v-else class="numRes"> Showing {{total_results}} of {{total_results}}</div>
       <div v-if="total_pages> 0" class="pagi">
      <span class="pagi_prev" @click="--page > 0 ? pagi(page) : ++page">&lt;</span>
      Page {{page}} of {{total_pages}}
      <span class="pagi_next" @click="++page < total_pages ? pagi(page) : --page">&gt;</span>
    </div>
      <div v-else class="no-results"> No results</div>
    <div class="movies" >
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
    <div v-if="total_pages > 0" class="pagi bottom">
      <span class="pagi_prev" @click="--page > 0 ? pagi(page) : ++page">&lt;</span>
      Page {{page}} of {{total_pages}}
      <span class="pagi_next " @click="page++ < total_pages ? pagi(page) : --page">&gt;</span>
    </div>
    <div v-else class="pagi bottom alt"></div>
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
      data: [],
      total_results: 0,
      total_pages: 0,
    };
  },
  created() {
    this.getData()
  },
  methods: {
    async getData(page) {
      const data = await fetch(
      `https://api.themoviedb.org/3/discover/movie?primary_release_year=2019&page=${this.page}&api_key=9084eae9f770e006ebcba95dbd474e28`
    ).then(response => response.json()).then(data => {
      this.data = data.results
      this.total_results = data.total_results
      this.total_pages = data.total_pages
    })
    },
    pagi(page) {
        this.getData(page)
      },
    update(data) {
      this.data = data.results
      this.total_results = data.total_results
      this.total_pages = data.total_pages
    }
  }
};
</script>

<style lang="scss">

html,body  {
  background-color: #2f3235;
  margin: 0;
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #e2e2e2;
  margin-top: 2rem;
  z-index: 2;
  position: relative;
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
.pagi{
  margin: 1rem 0;
  &_next{
    cursor: pointer;
    font-size: 1.1rem;
    margin-left: 1rem;
  }
  &_prev{
    cursor: pointer;
    font-size: 1.1rem;
    margin-right: 1rem;
  }
}
.bottom {
  position: absolute;
  bottom: -10px;
  left: 0; 
  right: 0;
  margin:  0;
}
.no-results {
  margin: 1rem;
}
</style>
