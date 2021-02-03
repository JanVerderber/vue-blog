<template>
  <div v-if="error">{{ error }}</div>
  <div v-if="post" class="post">
      <h3>{{ post.title }}</h3>
      <p class="pre">{{ post.body }}</p>
      <br>
      <span v-for="tag in post.tags" :key="tag">
        <router-link :to="{ name: 'Tags', params: { tag: tag }}" class="tag-item">
            #{{ tag }}
        </router-link> 
      </span>
  </div>
</template>

<script>

export default {
  name: 'Details',
  props: ['id'],
  data() {
      return {
          post: '',
          error: ''
      }
  },
  mounted() {
        var storedPosts = localStorage.getItem('posts')

        if (storedPosts) {
            var posts = JSON.parse(storedPosts)

            for (var i = 0; i < posts.length; i++) {
                if (posts[i].id == this.id) {
                    this.post = posts[i];
                }
            }
        }
        else {
            this.error = "This post does not exist"
        }
    },
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
    .tag-item{
        color: #2c3e50;
        margin: 3px;
    }
    .tag-item:hover{
        color: #5e748a;
    }
</style>