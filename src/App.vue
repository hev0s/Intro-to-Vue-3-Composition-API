<script setup>
import { ref } from 'vue'
const product = ref('Socks')
const description = ref("Chaussettes confort premium")
const image = ref("./src/assets/images/socks_blue.jpeg")
const url = ref("https://www.cpnv.ch/")
const linkLabel = ref("Voir plus d’infos (CPNV)")
</script>

<template>
  <div class="product-display">
    <div class="product-container">
      <div class="product-image">
        <img src="./assets/images/socks_blue.jpeg">
      </div>
      <div class="product-info">
        <h1>{{ product }}</h1>
        <div class="product-description">
          <p>{{ description }}</p>
        </div>
        <div class="product-links">
          <a :href="url" target="_blank" rel="noopener noreferrer">
            <link rel="stylesheet" href="https://www.cpnv.ch/">https://www.cpnv.ch/
          </a>
        </div>
      </div>
    </div>
  </div>
</template>