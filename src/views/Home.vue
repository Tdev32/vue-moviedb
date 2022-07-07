<template>
  <header>
    <img src="../assets/thebatman.jpeg" alt="">
  </header>
  <Movies />
</template>

<script>
import Movies from '../components/Movies.vue'

export default {
  name: 'Home',
  components: { 
    Movies 
  }
}
</script>

<style scoped>
header > img {
  width: 100vw;
}
</style>
