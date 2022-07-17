<template>
  <div class="navigation">
    <div class="container flex">
      <h1>Vue Films</h1>
      <div id="nav">
        <router-link to="/">Home</router-link> |
        <router-link to="/about">About</router-link>
      </div>
    </div>
  </div>
  <router-view/>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

body {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

h1 {
  margin: 0;
  color: red;
}

.flex {
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 4rem;
}

.container {
  width: 80%;
  margin: 0 auto;
}

.navigation {
  background-color: #171717;
}

#nav a {
  display: inline-block;
  font-weight: bold;
  color: white;
}

#nav a.router-link-exact-active {
  color: red;
}

@media only screen and (max-width: 560px) {
  .navigation {
    margin: 0 auto;
  }
}
</style>
