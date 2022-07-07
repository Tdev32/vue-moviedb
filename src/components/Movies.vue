<template>
<!-- Search form -->
  <div class="search">
    <input type="search" ref="input" placeholder="Search movie titles...">
    <button @click="searchMovies">Search</button>
  </div>
  
  <!-- Movie list -->
    
  <div class="container">
    <ul class="movie-group" v-for="movie in movies.results" v-bind:key="movie.id">
      <li>
        <router-link :to="'/movie/' + movie.id">
          <img :src="imageUrl + movie.poster_path" alt="">
          <div class="text-background">
            <span class="movie-title">{{ movie.title }}</span>
          </div>
        </router-link>
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
      imageUrl: "https://image.tmdb.org/t/p/w300/",
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
    }
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
  position: relative;
  list-style-type: none;
}
img:hover {
  cursor: pointer;
}
.container {
  width: 1275px;
  margin: 0 auto;
  max-width: auto;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(25%, 1fr));
}
button {
  width: 6rem;
  color: white;
  margin-top: 2rem;
  margin-left: 0.4rem;
  background-color: red; /* #42b983 */
  padding: 12px;
  border: none;
  border-radius: 50px;
}

button:hover {
  cursor: pointer;
}

.movie-group {
  width: 60%;
}

.text-background {
  position: absolute;
  background-color: rgba(255, 0, 0, 0.6);
  width: 300px;
  height: 3rem;
  bottom: 6px;
}

.movie-title {
  display: block;
  width: 98.4%;
  color: white;
  padding-left: 5px;
  text-align: center;
  transform: translateY(50%);
}

a {
  text-decoration: none;
}

@media only screen and (max-width: 560px) {
  .container {
    margin: 0 auto;
    width: 60%;
    grid-template-columns: 1fr;
  }
  li > img {
    width: 150px;
  }
}

@media only screen and (max-width: 450px) {
  .container {
    margin: 0 auto;
    width: 70.5%;
    grid-template-columns: 1fr;
  }
  li > img {
    width: 150px;
  }
}

</style>