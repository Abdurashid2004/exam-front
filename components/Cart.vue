<template>
  <div class="container my-10">
    <div class="flex justify-between mb-10 items-center">
      <h4 class="font-bold text-[50px] max-md:text-[32px]">Корзина</h4>
    </div>
    <div
      v-if="products.length > 0"
      class="grid md:grid-cols-9 py-9 px-11 rounded-[20px] bg-second md:mt-10"
    >
      <p
        v-for="(header, index) in headers"
        :key="index"
        :class="index === 0 ? 'col-span-1' : 'col-span-2'"
        class="font-medium text-primary/50 mb-7"
      >
        {{ header }}
      </p>
      <div
        v-for="(item, index) in products"
        :key="index"
        class="py-4 col-span-9 grid grid-cols-9 items-center border-t pt-8 border-black/10"
      >
        <div class="pr-8 col-span-1 w-[150px]">
          <img :src="item.image" class="rounded-[12px] " alt="Image" />
        </div>
        <div class="flex flex-col pr-8 h-full col-span-2 justify-between">
          <p class="text-primary font-semibold line-clamp-2">
            {{ item.title }}
          </p>
          <p class="text-primary font-bold text-[20px]">{{ item.price }} ₽</p>
        </div>
        <p class="text-primary pr-8 col-span-2 line-clamp-3">Светильник RADUGA COMBO XS Промышленное освещение; 50Вт; 230В; S4; XS;</p>
        <p class="text-primary pr-8 col-span-2 line-clamp-3">
          RAD-COMBO-50/XXX/230/XXX/XXX/S4/XS
        </p>
        <div class="flex w-full col-span-2 justify-between items-center">
          <div class="flex gap-5 items-center">
            <span
              class="cursor-pointer text-2xl text-primary"
              @click="decrement(item.id)"
              >-</span
            >
            <span
              class="text-2xl py-[19px] px-[27px] border border-primary/10 rounded-[10px] text-primary"
              >{{ getCount(item.id) }}</span
            >
            <span
              class="cursor-pointer text-2xl text-primary"
              @click="increment(item.id)"
              >+</span
            >
          </div>
          <Icon
            icon="gg:trash"
            class="text-3xl text-primary cursor-pointer"
            @click="removeProduct(item.id)"
          />
        </div>
      </div>
    </div>
    <div v-else class="text-9xl text-primary/50 py-40 font-bold">
      <p class="text-center">No Products</p>
    </div>
    <div v-if="products.length > 0" class="p-6 rounded-[20px] bg-second mt-5">
      <h3 class="text-[32px] font-bold text-primary">Оформление</h3>
      <div
        class="grid grid-cols-1 md:grid-cols-3 gap-5 border-b border-primary/10 py-8"
      >
        <input
          v-for="(item, index) in order"
          :key="index"
          :type="index != order.length - 1 ? 'text' : 'email'"
          name=""
          :placeholder="item"
          class="py-[12px] px-5 border border-primary rounded-full bg-transparent mb-3 md:mb-0"
          id=""
        />
      </div>
      <h3 class="text-[32px] mt-[37px] font-bold text-primary">Доставка</h3>
      <div class="grid grid-cols-1 md:grid-cols-3 gap-8 mb-11">
        <input
          type="text"
          name=""
          placeholder="Адрес доставки"
          class="py-[14px] px-5 border col-span-2 border-primary rounded-full bg-transparent mb-3 md:mb-0"
          id=""
        />
        <textarea
          name=""
          placeholder="Комментарий"
          style="resize: none"
          class="py-[18px] px-5 border col-span-2 border-primary rounded-[30px] w-full bg-transparent"
          id=""
          cols="30"
          rows="6"
        ></textarea>
      </div>
    </div>

<div v-if="products.length > 0" class="p-6 rounded-[20px] bg-second mt-5">
  <h3 class="text-[32px] font-bold text-primary">Оплата</h3>
  <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4">
    <div class="flex items-center mt-8">
      <label for="prod" class="text-primary/50 font-semibold">
        Товары
        <input
          name="prod"
          type="text"
          placeholder="......................................."
          class="text-primary/50 bg-transparent font-semibold"
        />
      </label>
      <p class="text-primary/50 font-semibold">{{ TotalCost() }} ₽</p>
    </div>
    <div class="flex items-center mt-8">
      <label for="prod" class="text-primary/50 font-semibold">
        Доставка
        <input
          name="prod"
          type="text"
          placeholder=".........................................."
          class="text-primary/50 bg-transparent font-semibold px-1"
        />
      </label>
      <p class="text-primary/50 font-semibold">
        {{ (15 / 100) * Number(TotalCost()) }} ₽
      </p>
    </div>
    <h3 class="text-primary font-bold col-span-full text-2xl mt-10 pb-5 sm:col-span-2 lg:col-span-3">
      {{ Number(TotalCost()) + Number((15 / 100) * Number(TotalCost())) }} ₽
    </h3>
    <button @click="btn()" class="w-full py-[14px] bg-primary text-white font-medium rounded-full">
      Купить
    </button>
    <div class="flex gap-[8px] items-center ml-7">
      <input type="radio" class="text-primary" />
      <p class="text-sm font-semibold">
        Я согласен на обработку моих персональных данных
      </p>
    </div>
  </div>
</div>

  </div>
</template>

<script setup>
import { Icon } from "@iconify/vue";
import { ref, onMounted } from "vue";
import { usePiniaStore } from "../store";

const store = usePiniaStore();
const products = ref([]);
const counts = ref({});

const headers = ["Фото", "Товары", "Описание", "Артикул", "Артикул"];

const order = ref(["ФИО", "телефон", "Электронная почта"]);

onMounted(() => {
  products.value = store.basket.map((product) => ({
    ...product,
    count: getCount(product.id), // Initialize count for each product
  }));
});

function btn() {
  alert("successfully!");
}

const removeProduct = (productId) => {
  const index = products.value.findIndex((item) => item.id === productId);
  if (index !== -1) {
    store.removeFromBasket(productId);
    products.value.splice(index, 1);
  }
};

const getCount = (productId) => counts.value[productId] || 1;

const increment = (productId, price) => {
  counts.value[productId] = counts.value[productId]
    ? counts.value[productId] + 1
    : 1;
    
};

const decrement = (productId) => {
  if (counts.value[productId] && counts.value[productId] > 1) {
    counts.value[productId]--;
  }
};

const TotalCost = () => {
  let total = 0;
  products.value.forEach((item) => {
    total += item.price * getCount(item.id);
  });
  store.totalPrice = total.toFixed(2);
  return total.toFixed(2);
};
</script>

<style scoped>
input,
textarea {
  outline: none;
}
/* Add your custom styles here */
</style>
