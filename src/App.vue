<script setup>
import { ref } from 'vue'
const product = ref("Chaussettes")
const description = ref("Chaussettes confort premium pour l’entraînement (matière respirante).")
const image = ref("./src/assets/images/socks_blue.jpeg")
const url = ref("https://www.cpnv.ch/")
const linkLabel = ref("Voir plus d’infos (CPNV)")
const inStock = ref(false)
const inventory = ref(11)
const onSale = ref(true)
</script>

<template>
  <div class="product-display">
    <div class="product-container">
      <div class="product-info">
        <h1>{{product}}</h1>
      </div>
      <div class="product-image">
        <img src="./assets/images/socks_blue.jpeg">
      </div>
      <div class="product-description">
        <p>{{description}}</p>
      </div>
    </div>
    <div class="link">
      <a :href="url" target="_blank" rel="noopener noreferrer">
        <link rel="stylesheet" href="https://www.cpnv.ch/">https://www.cpnv.ch/
      </a>
    </div>
  </div>
</template>