<template>
  <div class="movie-background">
    <img :src="imageUrl + movies.backdrop_path" alt="" />
    <div class="movie-container">
      <img :src="imageUrl + movies.poster_path" alt="" />
      <div class="movie-details">
        <h2>{{ movies.original_title }}</h2>
        <p>{{ movies.release_date.slice(0, 4) }} &middot; {{ movies.runtime + ' minutes' }}</p>
        <p class="movie-summary">{{ movies.overview }}</p>
        <div class="movie-credits">
          <div class="actor-profile" v-for="credit in movies.credits.cast.slice(0, 7)" :key="credit.id">
            <img class="actors-img" :src="imageUrl + credit.profile_path" alt="">
            <span class="actor-name">{{ credit.original_name }}</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { onBeforeMount, ref } from 'vue'
import { useRoute } from 'vue-router'

export default {
  name: 'Movie',
  setup() {
    const route = useRoute()
    const movies = ref([])
    const API_KEY = ref("2f8ad00f27f59846e18f2a0fa95ac328")
    const baseURL = ref("https://api.themoviedb.org/3/")
    const imageUrl = ref("https://image.tmdb.org/t/p/original/") // Original image size I used was w300
    const url = ref(`${baseURL.value}movie/${route.params.id}?api_key=${API_KEY.value}&append_to_response=videos,credits`)

    onBeforeMount(() => {
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
.movie-background {
  position: relative;
}
.movie-container {
  position: absolute;
  top: 5rem;
  left: 9rem;
  width: 1100px;
  margin: 0 auto;
  display: flex;
  background-color: rgba(0, 0, 0, 0.8);
  padding: 30px;
}
.movie-container > img {
  width: 30%;
  border-radius: 5px;
}
.movie-details {
  color: white;
  margin-top: 0;
  padding: 0 20px;
}
.movie-background > img {
  width: 100%;
}
.movie-credits {
  width: 100%;
  display: flex;
  justify-content: space-between;
}
.actor-profile {
  width: 15%;
  display: flex;
  flex-direction: column;
}
.actor-name {
  margin-top: 6px;
  font-size: 10px;
  padding: 2px;
}
.actors-img {
  width: 80%;
  border-radius: 5px;
}

@media only screen and (max-width: 560px) {
  .movie-background {
    height: 81rem;
    background-color: #181818;
  }
  .movie-background > img {
    width: 160%;
    transform: translateX(-18%);
  }
  .movie-container {
    position: static;
    width: 70%;
    transform: translateY(-28%);
    flex-direction: column;
  }
  .movie-container > img {
    width: 100%;
    border-radius: 5px;
  }
  .movie-details {
    text-align: center;
  }
  .movie-credits {
    margin-top: 3rem;
    width: 100%;
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
  }
  .actor-profile {
    width: 30%;
    display: flex;
    flex-direction: column;
  }
  .actor-name {
    width: 60px;
    margin-top: 6px;
    font-size: 10px;
    text-align: center;
  }
}

</style>