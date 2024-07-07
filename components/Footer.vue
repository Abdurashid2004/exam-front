<template>
  <div class="bg-second py-[79px] max-md:py-10">
    <div class="container">
      <div class="flex max-md:flex-col max-md:gap-5 w-full justify-between">
        <div class="flex flex-col md:w-1/4 gap-[35px]">
          <img
            src="/MainLogo.svg"
            @click="navigateTo('/')"
            class="w-3/4 max-md:w-1/2 cursor-pointer"
            alt="logo"
          />
          <p class="text-primary text-2xl font-semibold">8 (800) 890-46-56</p>
          <img
            src="/card.png"
            class="w-3/4 max-md:w-1/2 cursor-pointer"
            alt="card"
          />
          <p
            class="font-semibold underline opacity-50 cursor-pointer"
            @click="navigateToPrivacyPolicy"
          >
            Политика конфиденциальности
          </p>
          <div class="flex gap-3">
            <button
              v-for="index in 3"
              :key="index"
              class="h-9 w-9 rounded-full border-2 border-primary text-primary font-semibold"
              @click="navigateToSocialNetwork('VK')"
            >
              VK
            </button>
          </div>
        </div>
        <div
          v-for="(category, categoryIndex) in categories"
          :key="categoryIndex"
          class="text-primary"
        >
          <h4 :class="categoryIndex === 2 ? 'text-transparent' : ''" class="mb-8">
            {{ category.title }}
          </h4>
          <p
            v-for="(info, infoIndex) in category.info"
            :key="infoIndex"
            @click="handleNavigation(categoryIndex, infoIndex)"
            class="cursor-pointer hover:underline mb-[27px] opacity-50"
          >
            {{ info }}
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { useRouter } from "vue-router";
import { ref } from "vue";

const router = useRouter();

const categories = ref([
  {
    title: "Покупателям",
    info: [
      "О компании",
      "Доставка и оплата",
      "Возврат",
      "Гарантии",
      "Контакты",
      "Блог",
    ],
  },
  {
    title: "Товары",
    info: [
      "Люстры",
      "Светильники",
      "Бра",
      "Торшеры",
      "Комплектующие",
      "Настольные лампы",
    ],
  },
  {
    title: "Товары",
    info: [
      "Споты",
      "Трековые светильники",
      "Уличные светильники",
      "Технические светильники",
      "Светодиодные ленты",
    ],
  },
]);

const navigateTo = (path) => {
  router.push(path);
};

const navigateToPrivacyPolicy = () => {

};

const navigateToSocialNetwork = (network) => {

};

const handleNavigation = (categoryIndex, infoIndex) => {
  const routes = [
    ["/company", "/deliver", "/return", "/guarantees", "/contact", "/blogs"],
  ];

  if (routes[categoryIndex] && routes[categoryIndex][infoIndex]) {
    router.push(routes[categoryIndex][infoIndex]);
  }
};
</script>

<style lang="scss" scoped></style>
