<script setup>
const emit = defineEmits(['openDrawer']);


</script>

<template>
    <header class="flex justify-between border-b-4 border-stone-400 px-8 py-4 gap-8">
      <div class="flex items-center gap-4">
        <img src="/logo.png" alt="Logo" class="w-10" />
        <div>
          <h2 class="text-xl font-bold uppercase">Store</h2>
          <p class="text-slate-700">Best store in town</p>
        </div>
      </div>
      <ul class="flex items-center gap-10">
        <li @click="$emit('openDrawer')" class="flex items-center cursor-pointer gap-3 text-gray-500 hover:text-black">
          <img src="/cart.svg" alt="Cart" />
          <b>200 $</b>
        </li>
        <li
          class="flex items-center cursor-pointer gap-3 text-gray-500 hover:text-black"
          @click="$emit('showBookmarks')"
        >
          <img src="/heart.svg" alt="Heart" />
          <span>Bookmarks</span>
        </li>
        <li class="flex items-center cursor-pointer gap-3 text-gray-500 hover:text-black">
          <img src="/profile.svg" alt="Profile" />
          <span>Profile</span>
        </li>
      </ul>
    </header>
  </template>
  