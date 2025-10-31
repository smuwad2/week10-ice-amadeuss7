<script setup>
import blogPost from './subcomponents/BlogPost2.vue'
import axios from 'axios'
</script>

<script>
export default {
  data() {
    return {
      posts: [] // list of blog post objects
    }
  },
  components: {
    blogPost
  },
  computed: {
    baseUrl() {
      if (window.location.hostname === 'localhost') {
        return 'http://localhost:3000'
      } else {
        const codespace_host = window.location.hostname.replace('5173', '3000')
        return `https://${codespace_host}`
      }
    }
  },
  async created() {
    try {
      const response = await axios.get(`${this.baseUrl}/posts`)
      this.posts = response.data
    } catch (error) {
      this.posts = [{ entry: 'There was an error: ' + error.message }]
    }
  },
  methods: {
    async deletePost(id) {
      try {
        // Delete post by ID
        await axios.get(`${this.baseUrl}/deletePost`, { params: { id } })

        // Fetch updated posts
        const response = await axios.get(`${this.baseUrl}/posts`)
        this.posts = [...response.data] // trigger reactivity

        // Let Vue update DOM before Playwright checks
        await this.$nextTick()
        await new Promise(resolve => setTimeout(resolve, 100))
      } catch (error) {
        console.error('Error deleting post:', error)
      }
    }
  }
}
</script>

<template>
  <div>
    <!-- render each post with blogPost component -->
    <blog-post
      v-for="post in posts"
      :key="post.id"
      :subject="post.subject"
      :entry="post.entry"
      :mood="post.mood"
    >
      <template #default>
        <button
          class="btn btn-primary mt-2"
          @click="deletePost(post.id)"
        >
          Delete
        </button>
      </template>
    </blog-post>
  </div>
</template>
