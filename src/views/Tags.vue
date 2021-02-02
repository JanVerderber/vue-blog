<template>
  <div v-if="error">{{ error }}</div>
  <div v-if="posts" class="post">
      <div class="post-list">
        <div v-for="post in posts" :key="post.id">
            <SinglePost :post="post" />
        </div>
      </div>
  </div>
  <div v-else>
      <p>No posts found...</p>
  </div>
</template>

<script>
import SinglePost from '../components/SinglePost.vue'

export default {
  name: 'Tags',
  props: ['tag'],
  components: { SinglePost },
  data() {
      return {
          posts: [],
          error: ''
      }
  },
  mounted() {
        var storedPosts = localStorage.getItem('posts')

        if (storedPosts) {
            var posts = JSON.parse(storedPosts)
            console.log(String(this.tag))
            
            for (var i = 0; i < posts.length; i++) {
                if (posts[i].tags.includes(this.tag)) {
                    this.posts.push(posts[i]);
                }
            }
        }
        else {
            this.error = "TEST..."
        }
    }
}
</script>

<style>
    .post {
        max-width: 1200px;
        margin: 0 auto;
    }
    .post p {
        color: #444;
        line-height: 1.5em;
        margin-top: 40px;
    }
    .pre {
        white-space: pre-wrap;
    }
</style>