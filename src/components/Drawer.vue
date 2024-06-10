<script setup>
import DrawerHead from './DrawerHead.vue'

</script>

<template>
  <div class="fixed top-0 left-0 h-full w-full bg-black z-10 opacity-70"></div>
  <div class="bg-white w-96 h-full fixed right-0 top-0 z-20 p-8">
    <DrawerHead />
    <CartItemList />
    
    <div class="flex flex-col gap-4 mt-7">
      <div class="flex gap-2 ">
        <span>Total:</span>
        <div class="flex-1 border-b border-dashed"></div>
        <b>4000$</b>
      </div>
   

   
      <div class="flex gap-2 ">
        <span>Tax 5%:</span>
        <div class="flex-1 border-b border-dashed"></div>
        <b>900$</b>
      </div>
      <button disabled="" class="mt-4 transition bg-lime-500 w-full cursor-pointer disabled:bg-slate-300 rounded-xl py-3 text-white hover:bg-lime-600 active:bg-lime-700">Checkout</button>
    </div>
  </div>
</template>
