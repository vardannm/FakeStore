<script setup>
import Card from './Card.vue';
import { defineProps, defineEmits } from 'vue';

const { products, bookmarkedProducts } = defineProps(['products', 'bookmarkedProducts']);
const emit = defineEmits(['toggleBookmark']);

const handleToggleBookmark = (product) => {
  emit('toggleBookmark', product);
};
</script>

<template>
  <div class="grid grid-cols-4 gap-4">
    <Card 
      v-for="product in products" 
      :key="product.id"
      :title="product.title"
      :image-url="product.image"
      :price="product.price"
      :isFavorite="bookmarkedProducts.some(item => item.id === product.id)"
      @clickFavorite="handleToggleBookmark(product)"
    />
  </div>
</template>
