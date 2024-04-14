<script setup>
import Card from './Card.vue'

import { ref } from 'vue'; // Importing ref from Vue
import axios from 'axios';
const products = ref([]); // Creating a reactive reference
axios.get('https://fakestoreapi.com/products')
  .then(response => {
    products.value = response.data;
  })
  .catch(error => {
    console.error('Error fetching products:', error);
  });
</script>

<template>
  <div class="grid grid-cols-4 gap-4">
    <!-- Loop through products and render a Card component for each product -->
    <Card v-for="product in products" :key="product.id"
      :title="product.title"
      :image-url="product.image"
      :price="product.price"
    />
  </div>
</template>