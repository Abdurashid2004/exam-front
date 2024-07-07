<template>
  <div class="container mt-[102px]">
    <div class="flex justify-between mb-10 items-center">
      <h4 class="font-bold text-[40px]">Каталог</h4>
      <nuxt-link to="/catalog">
        <div
          class="flex items-center py-[8px] group cursor-pointer gap-[10px] w-[220px] rounded-full border border-primary"
        >
          <p class="ml-12 font-medium text-primary">Весь каталог</p>
          <p class="text-2xl font-medium mb-1 text-primary">&rarr;</p>
        </div>
      </nuxt-link>
    </div>
    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-5">
      <div
        class="bg-second duration-300 cursor-pointer rounded-[20px] group pl-8 pr-2 w-full h-full flex items-center py-4 justify-between flex-col sm:flex-row"
        v-for="(item, index) in candles"
        :key="index"
      >
        <div class="flex flex-col h-full justify-between text-center sm:text-left">
          <p class="text-primary font-medium text-[20px]">
            {{ datas[index].title }}
          </p>
          <p class="text-primary font-medium text-sm group cursor-pointer">
            {{ datas[index].price }}
            <span class="ml-1 duration-300 font-medium text-xl">&rarr;</span>
          </p>
        </div>
        <img class="w-[55%] sm:w-[40%]" :src="item" alt="" />
      </div>
    </div>

    <div
      class="flex items-center py-[8px] mt-5 max-md:w-full cursor-pointer bg-primary group gap-[10px] w-[220px] rounded-full border border-primary"
    >
      <p class="ml-12 font-medium max-md:ml-24 text-white">Весь каталог</p>
      <p class="text-2xl font-medium mb-1 text-white">&rarr;</p>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const candles = ref([
  "/can1.png",
  "/can2.png",
  "/can3.png",
  "/can4.png",
  "/can5.png",
  "/can6.png",
]);

const datas = ref([
  {
    title: "Люстры",
    price: "От 540₽",
  },
  {
    title: "Светильники",
    price: "От 540₽",
  },
  {
    title: "Бра",
    price: "От 540₽",
  },
  {
    title: "Торшеры",
    price: "От 540₽",
  },
  {
    title: "Настольные лампы",
    price: "От 540₽",
  },
  {
    title: "Споты",
    price: "От 540₽",
  },
]);
</script>

<style scoped>
/* Add any custom styles if needed */
</style>
