<script>
    export default {
        // Add code if/as necessary
        // Hint: Add properties subject, entry and mood
        props:{
            subject:String,
            entry: String,
            mood:String
        },
        computed:{
        imgloc(){
            return `/assets/${this.mood.toLowerCase()}.png` 
            // use `` when you trying to combine strings with variables, `` its like 'hello' + 'world '
            // have to use toLowerCase() as its run in linux
        }
    }
}
</script>


<template>
    <!-- TODO: add your template code here. Use boostrap card --> 
    <div class="card" style="width: 18rem;">
  <img :src="imgloc" class="card-img-top" alt="...">
  <div class="card-body">
    <h5 class="card-title">{{ subject }}</h5>
    <p class="card-text">{{ entry }}</p>
    
  </div>
</div>
</template>

