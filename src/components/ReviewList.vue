<script setup>
import { toRefs } from 'vue'
const props = defineProps({
  reviews: {
    type: Array,
    required: true
  }
})

function formatDate(iso) {
  try {
    const d = new Date(iso)
    return d.toLocaleString()
  } catch {
    return iso
  }
}
</script>

<template>
  <div class="review-container">
    <h3>Commentaires:</h3>
    <ul>
      <li v-for="(rev, index) in reviews" :key="index" class="review-item">
        <p><strong>{{ rev.name }}</strong> — <em>{{ rev.rating }}/5</em></p>
        <p>{{ rev.review }}</p>
        <p>Recommande : <strong>{{ rev.recommend }}</strong></p>
        <small v-if="rev.date">Posté le : {{ formatDate(rev.date) }}</small>
        <hr />
      </li>
    </ul>
  </div>
</template>

<style scoped>
.review-container { max-width: 700px; margin-bottom: 16px; }
.review-item { padding: 8px 0; }
</style>
