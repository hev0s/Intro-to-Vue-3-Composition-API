<script setup>
import { ref, computed } from 'vue'

import socksGreenImage from '../assets/images/socks_green.jpeg'
import socksBlueImage from '../assets/images/socks_blue.jpeg'

// components reviews (place ces fichiers dans src/components/)
import ReviewForm from './ReviewForm.vue'
import ReviewList from './ReviewList.vue'

const props = defineProps({
  premium: {
    type: Boolean,
    required: true
  }
})
const emit = defineEmits(['add-to-cart', 'remove-to-cart'])
const product = ref('Socks')
const brand = ref('Vue Mastery')

const selectedVariant = ref(0)

const details = ref(['50% cotton', '30% wool', '20% polyester'])

const variants = ref([
  { id: 2234, color: 'green', image: socksGreenImage, quantity: 50 },
  { id: 2235, color: 'blue', image: socksBlueImage, quantity: 0 },
])

const title = computed(() => {
  return brand.value + ' ' + product.value
})

const image = computed(() => {
  return variants.value[selectedVariant.value].image
})

const inStock = computed(() => {
  return variants.value[selectedVariant.value].quantity > 0
})

const shipping = computed(() => {
  if (props.premium) {
    return 'Free'
  }
  else {
    return 5.99
  }
})

const addToCart = () => {
  emit('add-to-cart', variants.value[selectedVariant.value].id)
}

const removeFromCart = () => {
  emit('remove-to-cart', variants.value[selectedVariant.value].id)
}

const updateVariant = (index) => {
  selectedVariant.value = index
}

/* ---------- Reviews logic ---------- */
// liste des reviews (vide au départ)
const reviews = ref([])

// méthode appelée quand ReviewForm émet 'review-submitted'
function addReview(review) {
  reviews.value.push(review)
}
</script>

<template>
  <div class="product-display">
    <div class="product-container">
      <div class="product-image">
        <img :src="image" :alt="title">
      </div>
      <div class="product-info">
        <h1>{{ title }}</h1>
        <p v-if="inStock">In Stock</p>
        <p v-else>Out of Stock</p>
        <p>Shipping: {{ shipping }}</p>
        <ul>
          <li v-for="(detail, idx) in details" :key="idx">{{ detail }}</li>
        </ul>
        <div
            v-for="(variant, index) in variants"
            :key="variant.id"
            @mouseover="updateVariant(index)"
            class="color-circle"
            :style="{ backgroundColor: variant.color }"
        >
        </div>
        <button
            class="button"
            :class="{ disabledButton: !inStock }"
            :disabled="!inStock"
            v-on:click="addToCart"
        >
          Add to cart
        </button>
        <button
            class="button"
            :class="{ disabledButton: !inStock }"
            :disabled="!inStock"
            v-on:click="removeFromCart"
        >
          Remove from cart
        </button>
      </div>
    </div>

    <!-- Review list: n'affiche la boîte que s'il y a au moins 1 review -->
    <review-list v-if="reviews.length" :reviews="reviews" />

    <!-- Formulaire d'ajout d'avis (toujours affiché) -->
    <review-form @review-submitted="addReview" />
  </div>
</template>

<style scoped>
/* tu peux garder tes styles existants ; j'ajoute juste un rappel pour .color-circle */
.color-circle {
  width: 24px;
  height: 24px;
  border-radius: 50%;
  display: inline-block;
  margin-right: 6px;
  cursor: pointer;
}
/* disabledButton si nécessaire */
.disabledButton {
  opacity: 0.5;
  cursor: not-allowed;
}
</style>
