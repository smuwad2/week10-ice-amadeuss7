<script setup>
    // Import BlogPost component
    import blogPost from './subcomponents/BlogPost2.vue'
	import axios from 'axios'
</script>

<script>
    export default {
        data() {
            return {
                posts: [] // array of post objects
            }  
        },
        computed: {
            baseUrl() {
                if (window.location.hostname == 'localhost')
                    return 'http://localhost:3000'
                else {
                    const codespace_host = window.location.hostname.replace('5173', '3000')
                    return `https://${codespace_host}`;
                }
            }
        },
        created() { // created is a hook that executes as soon as Vue instance is created
            axios.get(`${this.baseUrl}/posts`)
            .then(response => {
                // this gets the data, which is an array
                this.posts = response.data
                console.log(response.data)
            })
            .catch(error => {
                this.posts = [{ entry: 'There was an error: ' + error.message }]
            })
        },
        methods: {
            deletePost(id) {
                axios.get(`${this.baseUrl}/deletePost`, { params: { id: id } })
                .then(() => {
                    // Remove the deleted post locally
                    this.posts = this.posts.filter(post => post.id !== id)
                    console.log(`Deleted post with ID ${id}`)
                })
                .catch(error => {
                    console.error('Error deleting post:', error)
                })
            }
            },
        components:{
            blogPost
        }
    }
</script>

<template>
   <!-- TODO: make use of the 'blog-post' component to display the blog posts -->
    <blogPost v-for="post in posts" :mood="post.mood" :entry="post.entry" :subject="post.subject" :id="post.id">
        <button class="btn btn-primary" @click="deletePost(post.id)">Delete</button>
    </blogPost> 

</template>

