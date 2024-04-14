<script setup>
import Header from './components/Header.vue';
import CardList from './components/CardList.vue';
import Drawer from './components/Drawer.vue';
import axios from 'axios';
import { ref } from 'vue';

const products = ref([]);

axios.get('https://fakestoreapi.com/products')
  .then(response => {
    products.value = response.data;
  })
  .catch(error => {
    console.error('Error fetching products:', error);
  });
</script>
<template >
    <!-- <Drawer /> -->
    <div class="bg-stone-100 w-4/5 mx-auto rounded-xl shadow-xl mt-10">
    <Header />
    <div class="p-10"> 
        <div class="flex justify-between items-center"> 
        <h2 class="text-3xl font-bold mb-8">Products</h2>
    <div class="flex gap-4"> 
        <select class="py-2 px-3 border rounded-md outline-none">
        <option>By Name</option>
        <option>By Price (Low to High)</option>
        <option>By Price (High to Low)</option>
    </select>
    
    
        <div class="relative"> 
        <img src="/search.svg" class="absolute left-4 top-3" alt="Search"/>
        <input placeholder="Search..." class="border rounded-md py-2 pl-11 pr-4 outline-none focus:border-gray-400"/>
    </div>
    </div>
    </div>
    <CardList :products="products" />
    </div>
    </div>
</template>

