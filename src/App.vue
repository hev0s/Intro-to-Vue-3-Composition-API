<script setup>
import { ref } from 'vue'
const product = ref('Socks')
const image = ref("./src/assets/images/socks_blue.jpeg")
</script>

<template>
  <div class="product-display">
    <div class="product-container">
      <div class="product-image">
        <img src="./assets/images/socks_blue.jpeg">
      </div>
      <div class="product-info">
        <h1>{{ product }}</h1>
      </div>
    </div>
  </div>
</template>