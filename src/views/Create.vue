<template>
    <h1>Create a new post</h1>
    <form @submit.prevent="handleSubmit">
        <label>Title:</label>
        <input type="text" required v-model="title"><br>

        <label>Body:</label><br>
        <textarea required v-model="body" rows="10" cols="55">
        </textarea><br>

        <label>Tags:</label><br>
        <i>Write a tag and then press ALT + "comma"</i>
        <input type="text" v-model="tempTag" @keyup.alt="addTag">
        <div v-for="tag in tags" :key="tag" class="pill">
            {{ tag }}<span style="color: red" @click="removeTag(tag)"> x</span>
        </div>

        <div class="submit">
            <button>Create Post</button>
        </div>
    </form>
</template>

<script>
export default {
    name: 'Create',

    data() {
        return {
            id: 0,
            title: '',
            body: '',
            tempTag: '',
            tags: [],
            posts: []
        }
    },
    mounted() {
        var storedPosts = localStorage.getItem('posts')

        if (storedPosts) {
            var jsonData = JSON.parse(storedPosts)
            this.posts = jsonData
            var latestId = jsonData[jsonData.length-1].id
            this.id = latestId + 1    // Add +1 to old newest ID for new object
        }
    },
    methods: {
        addTag(e) {
            if (e.key === ',' && this.tempTag) {
                if (!this.tags.includes(this.tempTag)) {
                    this.tags.push(this.tempTag)
                }                
                this.tempTag = ''
            }
        },
        removeTag(tagToRemove) {
            this.tags.splice(this.tags.indexOf(tagToRemove), 1);
        },
        handleSubmit() {
            const newPost = { id: this.id, title: this.title, body: this.body, tags: this.tags }
            this.posts.push(newPost)
            localStorage.setItem('posts', JSON.stringify(this.posts))

            this.id++
            this.title = ''
            this.body = ''

            alert("Post has been successfully added!");
        }
    }   
}
</script>

<style>
    form {
        max-width: 420px;
        margin: 30px auto;
        background: white;
        text-align: left;
        padding: 40px;
        border-radius: 10px;
    }
    label {
        color: #aaa;
        display: inline-block;
        margin: 25px 0 15px;
        font-size: 0.6em;
        text-transform: uppercase;
        letter-spacing: 1px;
        font-weight: bold;
    }
    i {
        color: #aaa;
        display: inline-block;
        margin: 25px 0 15px;
        font-size: 0.6em;
        letter-spacing: 1px;
    }
    input, select {
        display: block;
        padding: 10px 6px;
        width: 100%;
        box-sizing: border-box;
        border: none;
        border-bottom: 1px solid #ddd;
        color: #555;
    }
    input[type="checkbox"] {
        display: inline-block;
        width: 16px;
        margin: 0 10px 0 0;
        position: relative;
        top: 2px;
    }
    .pill {
        display: inline-block;
        margin: 20px 10px 0 0;
        padding: 6px 12px;
        background: #eee;
        border-radius: 20px;
        font-size: 12px;
        letter-spacing: 1px;
        font-weight: bold;
        color: #777;
        cursor: pointer;
    }
    button {
        background: #0b6dff;
        border: 0;
        padding: 10px 20px;
        margin-top: 20px;
        color: white;
        border-radius: 20px;
    }
    .submit {
        text-align: center;
    }
    .error {
        color: #ff0062;
        margin-top: 10px;
        font-size: 0.8em;
        font-weight: bold;
    }
</style>