<script>
    export default {
        // Add code if/as necessary
        // Hint: Add properties subject, entry and mood
        props:{
            entry: String,
            mood: String,
            subject: String,
        },
        computed:{
            folder_location(){
                console.log(this.mood)
                return `/assets/${this.mood.toLowerCase()}.png`
            }
        }
    }
</script>


<template>
    <!-- TODO: add your template code here. Use boostrap card --> 
     <div class="card" style="width: 18rem;margin-bottom: 10px;" >
        <img class="" :src="folder_location" alt="Card image cap">
        <h5 class="card-title">{{subject}}</h5>
         <p class="card-text">{{ entry }}</p>
    </div>

</template>

