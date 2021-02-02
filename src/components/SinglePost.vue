<template>
    <div class="post">
        <router-link class="blog-link" :to="{ name: 'Details', params: { id: post.id }}">
            <h3>{{ post.title }}</h3>
        </router-link>
        <p>{{ snippet }}</p>
        <span v-for="tag in post.tags" :key="tag">
            #{{ tag }}
        </span>
    </div>
    <br>
</template>

<script>
import { computed } from 'vue'

export default {
    props: ['post'],
    setup(props) {
        const snippet = computed(() => {
            return props.post.body.substring(0, 100) + '...'
        })

        return { snippet }
    }
}
</script>

<style>
.post {
    width: 60%;
    display: block;
    background-color: #bfbfbf;
    padding: 10px;
    border-radius: 10px;
    text-align: left;
}

.blog-link {
    color: #2c3e50;
    text-decoration: none;
}

.blog-link:hover {
    color: #5e748a;
    text-decoration: underline;
}
</style>