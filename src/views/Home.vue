<template>
  <div class="home">
    <h1>Home</h1>
    <div v-if="error">
      {{ error }}
    </div>
    <div v-if="posts.length">
      <PostList :posts="posts" />
    </div>
    <div v-else>Loading posts...</div>
  </div>
</template>

<script>
import PostList from '../components/PostList.vue'

export default {
  name: 'Home',
  components: { PostList },
  data() {
      return {
          posts: []
      }
  },
  mounted() {
        var storedPosts = localStorage.getItem('posts')

        if (storedPosts) {
            this.posts = JSON.parse(storedPosts)
        }
    },
}
</script>
