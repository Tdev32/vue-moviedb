<template>
<!-- Search form -->
  <div class="search">
    <input type="search" ref="input" placeholder="Search movie titles...">
    <button @click="searchMovies">Search</button>
  </div>
  
  <!-- Movie list -->
    
  <div class="container">
    <div class="movie-item" v-for="movie in movies.results" v-bind:key="movie.id">
      <router-link :to="'/movie/' + movie.id">
        <img class="movie-image" :src="imageUrl + movie.poster_path" alt="">
        <div class="text-background">
          <span class="movie-title">{{ movie.title }}</span>
        </div>
      </router-link>
    </div>
    
  </div>
</template>

<script>

export default {
  name: 'Movies',
  data() {
    return {
      API_KEY: "2f8ad00f27f59846e18f2a0fa95ac328",
      baseURL: "https://api.themoviedb.org/3/",
      imageUrl: "https://image.tmdb.org/t/p/original/",
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
input {
  padding: 12px;
  width: 12rem;
  height: auto;
  border-radius: 50px;
  border: 1px solid lightgray;
}
.movie-item {
  width: 20%;
  position: relative;
  text-align: center;
}
.movie-image {
  width: 96%;
  border-radius: 5px;
}
img:hover {
  cursor: pointer;
}
.container {
  width: 90%;
  margin: 0 auto;
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
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

.text-background {
  width: 96%;
  position: absolute;
  border-radius: 5px;
  background-color: rgba(255, 0, 0, 0.6);
  height: 3rem;
  bottom: 5.7px;
  left: 5px;
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
  .movie-item {
    position: relative;
    display: inline-block;
    width: 50%;
  }
  img {
    border-radius: 5px;
  }
  .text-background {
    width: 96.3%;
    height: 1.6rem;
    border-radius: 5px;
  }
  .movie-title {
    font-size: .6rem;
  }
  .container {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
    width: 100%;
    margin: 0 auto;
  }
}

</style>