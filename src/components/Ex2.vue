<script>
    // Import BlogPost component
    import blogPost from './subcomponents/BlogPost.vue'
	import axios from 'axios'
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
                if (window.location.hostname=='localhost')
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
        }
    }
</script>

<template>
    <!-- rmb to run npm run backend  -->
   <!-- TODO: make use of the 'blog-post' component to display the blog posts -->
    <blog-post v-for="post in posts" :subject="post.subject"
    :entry="post.entry" :mood="post.mood" :key="post.id">


    </blog-post>
</template>

