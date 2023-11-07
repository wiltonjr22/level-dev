<template>
  <div>
    <h2>New Post</h2>
    <div>
      <label for="title">Title:</label>
      <input id="title" v-model="title" />
      <br />
      <label for="body">Body:</label>
      <textarea id="body" v-model="body"></textarea>
      <br />
      <button @click="createPost">Create Post</button>
    </div>

    <h2>Posts</h2>
    <div v-for="post in posts" :key="post.id">
      <div>
        <h3>{{ post.title }}</h3>
        <p>{{ post.body }}</p>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import api from '../http.ts'

interface Post {
  id: number
  title: string
  body: string
}

export default defineComponent({
  data() {
    return {
      posts: [] as Post[],
      title: '',
      body: '',
    }
  },

  methods: {
    async loadPosts() {
      try {
        const response = await api.get('/posts')
        this.posts = response.data as Post[]
      } catch (error) {
        console.error('Failed to load posts:', error)
      }
    },

    clearForm() {
      this.title = ''
      this.body = ''
    },

    async createPost() {
      try {
        await api.post('/posts', { title: this.title, body: this.body })
        this.clearForm()
        await this.loadPosts()
      } catch (error) {
        console.error('Failed to create a post:', error)
      }
    },
  },

  async mounted() {
    this.clearForm()
    await this.loadPosts()
  },
})
</script>
