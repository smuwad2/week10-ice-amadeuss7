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
         components:{
            blogPost
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
            async deletePost(id) {
                try {
                    await axios.get(`${this.baseUrl}/deletePost`, {
                        params: { id: id }
                    });
                    const response = await axios.get(`${this.baseUrl}/posts`);
                    this.posts = [];
                    await this.$nextTick();
                    this.posts = response.data;
                    await this.$nextTick();
                } catch (error) {
                    console.error('Error deleting post:', error);
                }
            }
        }
    }
</script>

<template>
   <!-- TODO: make use of the 'blog-post' component to display the blog posts -->
 <blog-post v-for="post in posts" :subject="post.subject"
    :entry="post.entry" :mood="post.mood" :key="post.id">
    <button class="btn btn-primary"@click=deletePost(post.id)>Delete</button>

    </blog-post>
</template>

