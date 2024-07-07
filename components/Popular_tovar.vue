<template>
  <div class="container mt-[102px]">
    <div class="flex justify-between mb-10 items-center">
      <h4 class="font-bold text-[40px] max-md:text-[28px]">
        Популярные товары
      </h4>

      <div
        @click="navigateToAbout"
        class="flex max-md:hidden items-center py-[8px] group cursor-pointer gap-[10px] w-[220px] rounded-full border border-primary"
      >
        <p class="ml-12 font-medium text-primary">
          О компании
        </p>
        <p
          class="text-2xl font-medium mb-1 text-primary"
        >
          &rarr;
        </p>
      </div>
    </div>
    <div v-if="isLoading" class="text-3xl text-gray-500 text-center py-10">
      <Loading/>
    </div>
    <div v-else class="grid md:grid-cols-4 grid-cols-2 gap-2 md:gap-5">
      <ProductCard
        v-for="(item, index) in products.slice(0, 8)"
        :key="item.id"
        :data="item"
        @click="navigateProduct(item.id)"
      />
    </div>
    <div
      @click="navigate"
      class="flex md:hidden max-md:w-full items-center max-md:mt-5 py-[8px] cursor-pointer gap-[10px] hover:gap-4 duration-300 w-[220px] rounded-full border border-primary"
    >
      <p class="ml-12 max-md:ml-24 font-medium text-primary">О компании</p>
      <p class="text-2xl font-medium mb-1 text-primary">&rarr;</p>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import axios from "axios";
import { useRouter } from "vue-router";

const products = ref([]);
const isLoading = ref(true); 
const router = useRouter();

const navigate = () => {
  router.push("/all-products");
};

const navigateProduct = (productId) => {
  router.push(`/all-products/[id]`);
};


const fetchProducts = async () => {
  try {
    const response = await axios.get(
      `https://66856627b3f57b06dd4c9bbf.mockapi.io/products/products`
    );
    console.log(response.data);
    products.value = response.data;
    isLoading.value = false; 
  } catch (error) {
    console.error("Error products:", error);
    isLoading.value = false;
  }
};

onMounted(fetchProducts);
</script>
