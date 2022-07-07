<template>
  <div class="movie">
    <div class="movie-container">
      <img :src="imageUrl + movies.poster_path" alt="" />
      <div class="movie-details">
        <h2>{{ movies.original_title }}</h2>
        <p>{{ movies.release_date }} &middot; {{ movies.runtime + ' minutes' }}</p>
        <p class="movie-summary">{{ movies.overview }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import { onMounted, ref } from 'vue'
import { useRoute } from 'vue-router'

export default {
  name: 'Movie',
  setup() {
    const route = useRoute()
    const movies = ref([])
    const API_KEY = ref("2f8ad00f27f59846e18f2a0fa95ac328")
    const baseURL = ref("https://api.themoviedb.org/3/")
    const imageUrl = ref("https://image.tmdb.org/t/p/w300/")
    const url = ref(`${baseURL.value}movie/${route.params.id}?api_key=${API_KEY.value}&language=en-US`)

    onMounted(() => {
      fetch(url.value)
        .then(res => res.json())
        .then(data => movies.value = data)
        .catch(err => console.log(err.message))
    })

    return { url, movies, route, imageUrl }
  },
}
</script>

<style scoped>
.movie-container {
  width: 1100px;
  margin: 0 auto;
  display: flex;
  background-color: rgb(246, 246, 246);
  padding: 30px;
}
.movie-details {
  margin-top: 0;
  padding: 0 20px;
}
.movie {
  margin-top: 4rem;
}

@media only screen and (max-width: 560px) {
  .movie-container {
    width: 60%;
    flex-direction: column;
    align-items: start;
  }
  .movie-details {
    text-align: center;
  }
}

</style>