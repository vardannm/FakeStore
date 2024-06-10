<script setup>
import { defineProps } from 'vue';

const { title, imageUrl, price, isFavorite, onClickFavorite, onClickAdd } = defineProps({
  title: String,
  imageUrl: String,
  price: Number,
  isFavorite: Boolean,
  onClickFavorite: Function,
  onClickAdd: Function
});
</script>

<template>
  <div class="relative border bg-stone-200 border-slate-200 rounded-3xl p-8 cursor-pointer transition hover:-translate-y-2 hover:shadow-xl">
    <img 
      :src="isFavorite ? '/like-2.svg' : '/like-1.svg'" 
      alt="Like" 
      class="absolute top-8 left-8" 
      @click="onClickFavorite" 
    />
    <img :src="imageUrl" alt="Product Image" class="rounded-3xl" />
    <p class="mt-2">{{ title }}</p>
    <div class="flex justify-between mt-5">
      <div class="flex flex-col">
        <span class="text-slate-400">Price</span>
        <b>{{ price }} $</b>
      </div>
      <img :src="!isAdded ? '/plus.svg' : '/checked.svg'" alt="Plus" @click="onClickAdd" />
    </div>
  </div>
</template>
