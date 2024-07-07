<template>
  <div class="container my-20 max-md:my-10">
    <div class="flex max-md:hidden justify-between mb-10 items-center">
      <h4 class="font-bold text-[50px]">Блог</h4>
    </div>
    <div class="grid md:grid-cols-3 gap-5 max-md:hidden">
      <div
        class="w-full h-full flex flex-col-reverse gap-[29px] justify-between border-b border-primary/10 pb-8"
        v-for="(item, index) in products"
        :key="index"
      >
        <div class="flex flex-col gap-6 h-full justify-between">
          <div class="flex justify-between gap-5 w-full">
            <p class="text-primary line-clamp-2 font-medium text-[20px]">
              {{ item.title }}
            </p>
            <span
              class="hover:rotate-45 mr-5 cursor-pointer duration-300 font-medium text-3xl"
            >
              <svg
                width="18"
                height="18"
                viewBox="0 0 18 18"
                fill="none"
                xmlns="http://www.w3.org/2000/svg"
              >
                <path
                  d="M1 1H17M17 1V17M17 1L1 17"
                  stroke="black"
                  stroke-width="2"
                />
              </svg>
            </span>
          </div>
          <p class="text-primary font-medium text-sm">
            {{ item.date }}
          </p>
        </div>
        <img class="w-full rounded-md" :src="item.image" :alt="item.title" />
      </div>
    </div>
    <div class="md:hidden">
      <h4 class="font-bold text-[40px] mb-5">Блог</h4>
      <div class="grid md:grid-cols-3 gap-5">
        <div
          class="w-full h-full flex flex-col-reverse gap-[29px] justify-between border-b border-primary/10 pb-8"
          v-for="(item, index) in products"
          :key="index"
        >
          <div class="flex flex-col gap-6 h-full justify-between">
            <div class="flex justify-between gap-5 w-full">
              <p class="text-primary line-clamp-2 font-medium text-[20px]">
                {{ item.title }}
              </p>
              <span
                class="hover:rotate-45 mr-5 cursor-pointer duration-300 font-medium text-3xl"
              >
                <svg
                  width="18"
                  height="18"
                  viewBox="0 0 18 18"
                  fill="none"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <path
                    d="M1 1H17M17 1V17M17 1L1 17"
                    stroke="black"
                    stroke-width="2"
                  />
                </svg>
              </span>
            </div>
            <p class="text-primary font-medium text-sm">
              {{ item.date }}
            </p>
          </div>
          <img class="w-full rounded-md" :src="item.image" :alt="item.title" />
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import axios from "axios";

const products = ref([]);

onMounted(async () => {
  try {
    const response = await axios.get(
      `https://66856627b3f57b06dd4c9bbf.mockapi.io/products/blogs`
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

<style scoped>
/* Add your custom styles here */
</style>
