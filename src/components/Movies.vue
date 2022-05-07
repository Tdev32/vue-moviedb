<template>
  <div class="search">
    <input type="search" ref="input" placeholder="Search movie titles...">
    <button @click="searchMovies">Search</button>
  </div>
  <div class="movie-content">
    <ul class="movie-group" v-for="item in movies.results" v-bind:key="item.id">
      <li>
        <img :src="imageUrl + item.poster_path" alt="">
        {{ item.title }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'Movies',
  data() {
    return {
      API_KEY: "2f8ad00f27f59846e18f2a0fa95ac328",
      baseURL: "https://api.themoviedb.org/3/",
      imageUrl: "https://image.tmdb.org/t/p/w185/",
      movies: [],
    }
  },
  methods: {
    searchMovies() {
      const input = this.$refs.input;
      const url = `${this.baseURL}search/movie?api_key=${this.API_KEY}&query=${input.value}`;
      fetch(url)
        .then(res => res.json())
        .then(data => this.movies = data)
        .catch(err => console.log(err.message))
    },
    getter() {
      const input = this.$refs.input;
      console.log(input.value)
    },
  }
}
</script>

<style scoped>
.search {
  width: 19rem;
  margin: 0 auto 2rem auto;
}
ul, li {
  margin: 0;
  padding: 0;
}
input {
  padding: 12px;
  width: 12rem;
  height: auto;
  border-radius: 50px;
  border: 1px solid lightgray;
}
li {
  list-style-type: none;
}
.movie-content {
  margin: 0 auto;
  max-width: auto;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(185px, 1fr));
}
button {
  width: 6rem;
  color: white;
  margin-left: 0.4rem;
  background-color: #42b983;
  padding: 12px;
  border: none;
  border-radius: 50px;
}

</style>