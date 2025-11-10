<script setup>

import {computed, ref} from 'vue'
import ProductDisplay from "@/components/ProductDisplay.vue";

const cart = ref([])
const premium = ref(true)
// to stock items ids in cart
const CartItems = (id) => {
  cart.value.push(id)
}
// to show how many items in cart
const cartCountItems = computed(() => {
  return cart.value.length
})

</script>
  
<template>
  <div class="nav-bar"></div>
  <!-- Value to change to see if we want nbr items or ids -->
  <div class="cart">Cart({{ cartCountItems}})</div>
  <ProductDisplay :premium="premium" @add-to-cart="CartItems">
  </ProductDisplay>
</template>