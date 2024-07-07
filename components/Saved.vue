<template>
  <div class="container my-10">
    <div class="flex justify-between mb-10 items-center">
      <h4 class="font-bold text-[40px] max-md:text-[28px]">Избранные товары</h4>
    </div>
    <div v-if="products.length > 0" class="grid md:grid-cols-4 grid-cols-2 gap-2 md:gap-5">
      <ProductCard v-for="(item, index) in products" :key="index" :data="item" />
    </div>
    <div v-else class="text-center text-gray-500">
      <p class="text-9xl text-primary/50 py-40 font-bold text-center">No Saved</p>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import { usePiniaStore } from "../store";
 // Make sure to adjust the import path if necessary

const store = usePiniaStore();
const products = ref([]);

onMounted(() => {
  products.value = store.likedProducts;
});
</script>

<style scoped>
/* Your custom styles can go here */
</style>
