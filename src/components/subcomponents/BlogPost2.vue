<script>
    export default {
        // Add code if/as necessary
        // Hint: Add properties subject, entry and mood
        props:{
            entry: String,
            mood: String,
            subject: String,
            id: Number
        },
        computed:{
            url_link(){
                return `/assets/${this.mood.toLowerCase()}.png`
            }
        }
    }
</script>


<template>
    <!-- TODO: add your template code here Use boostrap card --> 
    <div class="card" style="width: 18rem;">
    <img class="card-img-top" :src="url_link" alt="Card image cap">
    <div class="card-body">
    <h5 class="card-title">{{ subject }}</h5>
    <p class="card-text">{{entry}}</p>
    <slot></slot>
  </div>
</div>
</template>