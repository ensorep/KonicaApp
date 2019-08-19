<template>
  <input @keyup="changeData" id="search" v-model="search" type="text" placeholder="Search for movies" />
</template>

<script>
export default {
  name: "Search",
  data() {
    return {
      search : "",
      searchdatas: []
    }
  },
  methods: {
    async changeData ()  {
      this.$emit("search", await this.updateData())
      },
    async updateData() {
      return await fetch(`https://api.themoviedb.org/3/search/movie?query=${this.search}&api_key=9084eae9f770e006ebcba95dbd474e28`)
        .then(response => response.json()).then(data =>this.searchdatas = data.results)
    }
    }
};
</script>

<style lang="scss" scoped>
#search {
  padding: 0.5rem 8rem .5rem 0.5rem;
  font-size: 1rem;
  margin-bottom: 1rem;
  border-radius: 5px;
  border: none;
}
</style>