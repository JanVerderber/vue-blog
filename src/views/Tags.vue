<template>
  <h1>Searching by tag: #{{ tag }}</h1>
  <div v-if="error">{{ error }}</div>
  <div v-if="posts" class="post">
      <div class="post-list">
        <div v-for="post in posts" :key="post.id">
            <router-link class="blog-link" :to="{ name: 'Details', params: { id: post.id }}">
                <h3>{{ post.title }}</h3>
            </router-link>
            <p>{{ post.body }}</p>
            <span v-for="tag in post.tags" :key="tag">
                <router-link :to="{ name: 'Tags', params: { tag: tag }}" class="tag-item" @click="changeTagSearch(tag)">
                    #{{ tag }}
                </router-link>            
            </span>
            <br>
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
        
        for (var i = 0; i < posts.length; i++) {
            if (posts[i].tags.includes(this.tag)) {
                this.posts.push(posts[i]);
            }
        }
    }
    else {
        this.error = "No posts found..."
    }
  },
  methods: {
      changeTagSearch(tag) {
          this.tag = tag
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