<script setup>
import { ref } from 'vue'
import socksGreenImage from './assets/images/socks_green.jpeg'
import socksBlueImage from './assets/images/socks_blue.jpeg'
const product = ref('Socks')
const inStock = false
const onSale = false
const inventory = 1
const image = ref(socksGreenImage)

</script>
  
<template>
  <div class="nav-bar"></div>
  <div class="product-display">
    <div class="product-container">
      <div class="product-image">    
        <img v-bind:src="image">
      </div>
      <div class="product-info">
        <h1>{{ product }}</h1>
        <p v-if="inStock">En stock</p>
        <p v-else>En rupture de stock</p>
        <p v-if="inventory > 10">En stock</p>
        <p v-else-if="inventory >= 1">Faible stock</p>
        <p v-else-if="inventory >= 0">En rupture de stock</p>
        <p v-if="onSale">En solde</p>
      </div>
    </div>
  </div>
</template>