<template>
  <div class="container">
    <pre>{{ products }}</pre>
  </div>
</template>

<script setup>
const products = ref([]);
import { ref, onMounted } from 'vue';
import axios from 'axios';


onMounted(async () => {
  try {
    const response = await axios.get(
      `https://667d5f3b297972455f64d6c6.mockapi.io/products/products`
    );
    products.value = response.data.map((product) => ({
      ...product,
      liked: false,
      shopped: false,
    }));
  } catch (error) {
    console.error("Error products:", error);
  }
});
</script>
