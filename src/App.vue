<template>
  <br>
  <nav id="main-nav">
    <router-link class="main-nav-item" :to="{ name: 'Home' }">Home</router-link> |
    <router-link class="main-nav-item" :to="{ name: 'Create' }">Create new post</router-link>
  </nav>
  <br>
  <router-view/>  
</template>

<style>
body {
  background-color: #f2f2f2;
  margin: 0;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#main-nav {
  width: 20%;
  margin: auto;
  border-radius: 10px;
  padding: 10px;
  background-color: grey;
  font-size: 20px;

}

.main-nav-item {
  color: white;
  padding: 5px;
  text-decoration: none;
}

.main-nav-item:hover {
  color: #609af7;
  cursor: pointer;
}
</style>
