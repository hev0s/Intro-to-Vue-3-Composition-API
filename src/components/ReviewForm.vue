<script setup>

</script>

<template>
  <form class="review-form" @submit.prevent="onSubmit">
    <h3>Laissez un commentaire</h3>

    <label for="name">Nom:</label>
    <input id="name" v-model="name" />

    <label for="review">Commentaire:</label>
    <textarea id="review" v-model="review"></textarea>

    <label for="rating">Note:</label>
    <select id="rating" v-model.number="rating">
      <option value="5">5</option>
      <option value="4">4</option>
      <option value="3">3</option>
      <option value="2">2</option>
      <option value="1">1</option>
    </select>

    <label for="recommend">Recommanderiez-vous ce produit ?</label>
    <select id="recommend" v-model="recommend">
      <option value="">--Choisir--</option>
      <option value="Yes">Yes</option>
      <option value="No">No</option>
    </select>

    <input class="button" type="submit" value="Valider" />
  </form>
</template>

<script setup>
import { ref } from 'vue'

// définit l'événement émis vers le parent
const emit = defineEmits(['review-submitted'])

// champs du formulaire
const name = ref('')
const review = ref('')
const rating = ref(null)
const recommend = ref('') // "Yes" / "No"

function onSubmit() {
  // validation simple
  if (!name.value || !review.value || rating.value === null || recommend.value === '') {
    alert('Un des champs est vide. Veuillez indiquer votre nom, votre avis et une note');
    return;
  }

  const productReview = {
    name: name.value,
    review: review.value,
    rating: rating.value,
    recommend: recommend.value,
    date: new Date().toISOString() // optionnel : pour afficher la date
  };

  emit('review-submitted', productReview);

  // reset champs
  name.value = ''
  review.value = ''
  rating.value = null
  recommend.value = ''
}
</script>

<style scoped>
.review-form {
  max-width: 520px;
  display: flex;
  flex-direction: column;
  gap: 8px;
}
.review-form input[type="text"],
.review-form textarea,
.review-form select {
  padding: 6px;
  font-size: 14px;
}
.button { margin-top: 8px; padding: 8px 12px; cursor: pointer; }
</style>


