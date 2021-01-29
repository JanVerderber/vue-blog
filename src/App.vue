<template>
  <router-link :to="{ name: 'Home' }">Home</router-link>
  |<router-link :to="{ name: 'Create' }">Create new post</router-link>
  <router-view/>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
