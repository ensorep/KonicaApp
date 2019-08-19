<template>
  <input v-model="query" @keyup="changeData" id="search" type="text" placeholder="Search for movies" />
</template>

<script>
export default {
  name: "Search",
  data () {
    return {
      query: "",
    }
  },
  methods: {
    async changeData ()  {
      this.$emit("search", await this.updateData())
      },
    async updateData() {
      if(!this.query.length){
        return await fetch(`https://api.themoviedb.org/3/discover/movie?primary_release_year=2019&page=1&api_key=9084eae9f770e006ebcba95dbd474e28`)
        .then(response => response.json())
      }
      return await fetch(`https://api.themoviedb.org/3/search/movie?query=${this.query}&api_key=9084eae9f770e006ebcba95dbd474e28`)
        .then(response => response.json())
    }
  }
};
</script>

<style lang="scss" scoped>
#search {
  padding: 0.5rem 8rem .5rem 0.5rem;
  font-size: 1rem;
  margin: auto;
  margin: 1rem 0;
  border-radius: 5px;
  border: none;
  display: block;
  margin: 1rem auto;
}
</style>