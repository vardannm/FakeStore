<template>
  <Drawer v-if="drawerOpen" />
  <div class="bg-stone-100 w-4/5 mx-auto rounded-xl shadow-xl mt-10">
    <Header @showBookmarks="showBookmarksView" @openDrawer="openDrawer" />
    <div class="p-10">
      <div class="flex justify-between items-center">
        <h2 class="text-3xl font-bold mb-8">
          {{ isShowingBookmarks ? 'Bookmarked Products' : 'Products' }}
        </h2>
        <div v-if="!isShowingBookmarks" class="flex gap-4">
          <input
            v-model="searchTerm"
            @input="applySearch"
            type="text"
            placeholder="Search products"
            class="py-2 px-3 border rounded-md outline-none"
          />
          <select @change="onChangeCategory" class="py-2 px-3 border rounded-md outline-none">
            <option value="/">All Products</option>
            <option value="/category/jewelery">Jewelery</option>
            <option value="/category/electronics">Electronics</option>
            <option value="/category/men's%20clothing">Men's clothing</option>
            <option value="/category/women's%20clothing">Women's clothing</option>
          </select>
          <select @change="onChangeSort" class="py-2 px-3 border rounded-md outline-none">
            <option value="">Default</option>
            <option value="name">By Name</option>
            <option value="price">By Price</option>
          </select>
        </div>
      </div>
      <CardList
        :products="displayedProducts"
        :bookmarkedProducts="bookmarkedProducts"
        @toggleBookmark="toggleBookmark"
      />
    </div>
  </div>
</template>

<script setup>
import { ref, computed, watch , provide} from 'vue'
import axios from 'axios'
import Header from './components/Header.vue'
import CardList from './components/CardList.vue'
import Drawer from './components/Drawer.vue'

const drawerOpen = ref(false)

const closeDrawer =()=>{
  drawerOpen.value = false;
}
const openDrawer =()=>{
  drawerOpen.value = true;
}
const originalProducts = ref([])
const products = ref([])
const bookmarkedProducts = ref([])
const sortBy = ref('')
const sortMethod = ref('')
const searchTerm = ref('')
const isShowingBookmarks = ref(false)

const fetchProducts = async () => {
  try {
    let url = 'https://fakestoreapi.com/products'
    if (sortBy.value) {
      url += sortBy.value
    }
    const response = await axios.get(url)
    originalProducts.value = response.data
    products.value = [...originalProducts.value] // Clone to ensure reactivity
    applySorting()
  } catch (error) {
    console.error('Error fetching products:', error)
  }
}

const applySorting = () => {
  if (sortMethod.value === 'name') {
    products.value.sort((a, b) => a.title.localeCompare(b.title))
  } else if (sortMethod.value === 'price') {
    products.value.sort((a, b) => a.price - b.price)
  } else {
    products.value = [...originalProducts.value] // Reset to original if no sort
  }
  applySearch()
}

const applySearch = () => {
  if (searchTerm.value) {
    products.value = originalProducts.value.filter((product) =>
      product.title.toLowerCase().includes(searchTerm.value.toLowerCase())
    )
  } else {
    products.value = [...originalProducts.value]
  }
}

const onChangeCategory = (event) => {
  sortBy.value = event.target.value
  fetchProducts()
}

const onChangeSort = (event) => {
  sortMethod.value = event.target.value
  applySorting()
}

const toggleBookmark = (product) => {
  const index = bookmarkedProducts.value.findIndex((item) => item.id === product.id)
  if (index !== -1) {
    bookmarkedProducts.value.splice(index, 1) // Remove bookmark
  } else {
    bookmarkedProducts.value.push(product) // Add bookmark
  }
}

const showBookmarksView = () => {
  isShowingBookmarks.value = !isShowingBookmarks.value
}

watch(sortBy, fetchProducts)
watch(sortMethod, applySorting)

const filteredProducts = computed(() => {
  return products.value.filter((product) =>
    product.title.toLowerCase().includes(searchTerm.value.toLowerCase())
  )
})

const displayedProducts = computed(() => {
  return isShowingBookmarks.value ? bookmarkedProducts.value : filteredProducts.value
})

// Initial fetch
fetchProducts()
provide('cartActions',{closeDrawer,openDrawer});
</script>
