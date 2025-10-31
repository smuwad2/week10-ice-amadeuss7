<script>
export default {
  props: {
    subject: String,
    entry: String,
    mood: String
  },
  computed: {
    imgloc() {
      return `/assets/${this.mood?.toLowerCase() || 'neutral'}.png`
    }
  }
}
</script>

<template>
  <div class="card mb-3" style="width: 18rem;">
    <img :src="imgloc" class="card-img-top" alt="mood image" />
    <div class="card-body">
      <h5 class="card-title">{{ subject }}</h5>
      <p class="card-text">{{ entry }}</p>
      <slot></slot>
    </div>
  </div>
</template>
