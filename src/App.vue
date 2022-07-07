<template>
  <div class="navigation">
    <h1>Vue Films</h1>
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
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
  color: red;
  padding: 0 80px;
}

.navigation {
  background-color: #171717;
  display: flex;
}

#nav {
  width: 8rem;
  margin-left: auto;
  padding: 30px 60px;
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
    flex-direction: column;
  }
  h1 {
    width: 100%;
    padding: 0;
    text-align: center;
  }
  #nav {
    width: 6.5rem;
    padding: 0 0 30px 0;
    margin: 0 auto;
  }
}

@media only screen and (max-width: 430px) {
  .navigation {
    flex-direction: column;
  }
  h1 {
    width: 100%;
    padding: 0;
    text-align: center;
  }
  #nav {
    width: 6.7rem;
    padding: 0 0 30px 0;
    margin: 0 auto;
  }
}
</style>
