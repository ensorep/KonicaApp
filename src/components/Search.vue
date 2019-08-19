<template>
  <input id="search" v-model="search" type="text" placeholder="Search for movies" />
</template>

<script>
export default {
  name: "Search",
  data() {
    return {
      search: "",
      getData: () => {
        const data = fetch(
          `https://api.themoviedb.org/3/search/?${search}&api_key=9084eae9f770e006ebcba95dbd474e28`
        );
        data
          .then(response => response.json())
          .then(data => (this.movies = data.results));
        //need to set page back to one
        //also need to send data to parent via $emit
      }
    };
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