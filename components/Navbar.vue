<template>
  <div class="container md:pt-3">
    <div
      class="hidden md:flex w-full justify-between mb-2 text-primary font-semibold text-sm"
    >
      <div class="flex gap-7">
        <a
          v-for="(section, index) in sections"
          :key="index"
          :href="section.path"
          @click.prevent="handle(section.path)"
          class="opacity-50 hover:opacity-100 transition-opacity duration-200"
        >
          {{ section.name }}
        </a>
      </div>
      <div class="flex gap-6">
        <p class="opacity-100">8 (800) 890-46-56</p>
        <a
          href="#"
          @click="toggleModal"
          class="opacity-50 hover:opacity-100 transition-opacity duration-200"
          >Заказать звонок</a
        >
      </div>
    </div>
  </div>

  <div
    :class="[
      'sticky top-0 left-0 w-full py-3 z-30 transition-all duration-300',
      isScrolled && !toggle
        ? 'backdrop-blur-lg bg-gradient-to-r from-white to-gray-100'
        : 'bg-white',
    ]"
  >
    <div class="container">
      <div class="flex w-full justify-between items-center gap-4">
        <div class="flex md:gap-[29px] gap-4">
          <img
            @click="toggle = !toggle"
            :src="!toggle ? '/res_open.svg' : '/res_close.svg'"
            :class="toggle ? 'w-[20px]' : ''"
            class="block md:hidden duration-300 cursor-pointer w-[25px]"
            alt="Menu"
          />
          <img
            @click="Home"
            src="/MainLogo.svg"
            class="cursor-pointer hidden md:block w-64"
            alt="Logo"
          />
          <img
            @click="Home"
            :class="[
              'cursor-pointer md:hidden w-[75%]',
              { hidden: toggle, block: !toggle },
            ]"
            src="/MainLogo.svg"
            alt="Logo"
          />
          <div
            @click="handle('/catalog')"
            class="hidden md:flex px-[27px] gap-[9px] cursor-pointer items-center rounded-full bg-primary hover:bg-slate-700 text-white py-[14px]"
          >
            <img src="/catalog.svg" alt="category" class="w-[20px] h-[20px]" />
            <p class="font-semibold">Каталог</p>
          </div>
        </div>
        <div class="relative hidden md:block w-[45%]">
          <input
            type="text"
            placeholder="Поиск по товарам"
            class="font-semibold bg-white/50 outline-none pl-[27px] pr-12 h-full py-[12px] placeholder:text-primary border border-primary rounded-full w-full"
          />
          <img
            class="absolute top-1/2 -translate-y-1/2 right-0 -translate-x-3/4 z-10"
            src="/search.svg"
            alt="search"
          />
        </div>
        <div
          class="hidden md:flex h-full items-center gap-4"
          v-for="(item, index) in image"
          :key="index"
        >
          <div class="relative flex flex-col items-center gap-[6px]">
            <span
              v-if="
                index !== 1 &&
                (index === 0
                  ? store.likedProducts.length > 0
                  : store.basket.length > 0)
              "
              :class="{ '-translate-x-1/4': index === 0 }"
              class="absolute -translate-y-1/2 top-0 w-5 h-5 flex justify-center items-center rounded-full right-0 bg-red-500 z-50 text-white text-sm"
            >
              {{
                index === 0 ? store.likedProducts.length : store.basket.length
              }}
            </span>
            <img
              @click="
                index === 0
                  ? handle('/save')
                  : index === 2
                  ? handle('/bucket')
                  : null
              "
              :src="item"
              :class="index + 1 !== image.length ? 'w-1/3' : 'w-1/2'"
              class="cursor-pointer"
              alt="Logos"
            />
            <p class="text-[12px] font-semibold text-primary">
              {{ bottom[index] }}
            </p>
          </div>
        </div>
        <div class="flex items-center gap-2">
          <div
            class="flex relative h-full md:hidden items-center"
            v-for="(item, index) in image"
            :key="index"
          >
            <span
              v-if="
                index !== 1 &&
                (index === 0
                  ? store.likedProducts.length > 0
                  : store.basket.length > 0)
              "
              :class="{
                '-translate-y-[65%] right-0 translate-x-1': index === 0,
              }"
              class="absolute -translate-y-1/2 top-0 w-4 h-4 flex justify-center items-center rounded-full right-0 bg-red-500 z-50 text-white text-[10px]"
            >
              {{
                index === 0 ? store.likedProducts.length : store.basket.length
              }}
            </span>
            <img
              @click="
                index === 0
                  ? handle('/save')
                  : index === 2
                  ? handle('/bucket')
                  : null
              "
              :src="item"
              :class="{
                'w-3/4 mb-0.5': index === 2,
                block: index === 1 && toggle,
                hidden: index === 1 && !toggle,
              }"
              class="cursor-pointer"
              alt="Logos"
            />
          </div>
        </div>
      </div>
      <div class="relative md:hidden w-full mt-2">
        <input
          type="text"
          placeholder="Поиск по товарам"
          class="font-semibold text-sm bg-white/50 outline-none pl-[27px] pr-12 h-full py-[10px] placeholder:text-primary border py-[10px] border-primary rounded-full w-full"
        />
        <img
          class="absolute top-1/2 -translate-y-1/2 right-0 -translate-x-3/4 z-10"
          src="/search.svg"
          alt="search"
        />
      </div>
    </div>
  </div>

  <div
    :class="[
      'fixed z-50 top-[95px] left-0 w-full transition-all duration-300 md:hidden',
      { 'scale-0 h-0': !toggle, 'scale-100 h-full': toggle },
    ]"
  >
    <div class="container bg-white pb-8">
      <a
        v-for="(section, index) in sections"
        :key="index"
        href="#"
        @click="toggleMenu(index)"
        class="block pt-8 text-center mx-auto border-b w-full text-primary text-sm border-b-primary/50 transition-all duration-300"
      >
        {{ section.name }}
      </a>
      <div
        @click="toggleMenu('catalog')"
        class="flex justify-center w-full gap-[9px] cursor-pointer items-center rounded-full bg-primary mt-6 py-[14px]"
      >
        <img src="/catalog.svg" alt="category" />
        <p class="text-white font-semibold">Каталог</p>
      </div>
      <div class="flex flex-col gap-4 mt-8 justify-center w-full">
        <p class="text-center">8 (800) 890-46-56</p>
        <p @click="toggleModalAndMenu" class="text-center cursor-pointer">
          Заказать звонок
        </p>
      </div>
    </div>
    <div
      @click.stop="toggle = !toggle"
      :class="{ hidden: !toggle, block: toggle }"
      class="h-screen duration-300 w-screen bg-primary/50"
    ></div>
  </div>
</template>

<script setup>
import { usePiniaStore } from "../store";
import { ref, onMounted, onUnmounted } from "vue";
import { useRouter } from "vue-router";

const store = usePiniaStore();
const router = useRouter();

const toggle = ref(false);
const isScrolled = ref(false);

const sections = ref([
  { name: "О компании", path: "/about-us" },
  { name: "Доставка и оплата", path: "/deliver" },
  { name: "Возврат", path: "/return" },
  { name: "Гарантии", path: "/garante" },
  { name: "Контакты", path: "/contacts" },
  { name: "Блог", path: "/blogs" },
]);

const bottom = ref(["Избранное", "Сравнение", "Корзина"]);
const image = ref(["/like5.svg", "/compare.svg", "/cart.svg"]);

const handleScroll = () => {
  isScrolled.value = window.scrollY > 0;
};

onMounted(() => {
  window.addEventListener("scroll", handleScroll);
});

onUnmounted(() => {
  window.removeEventListener("scroll", handleScroll);
});

const Home = () => {
  router.push("/");
};

const handle = (path) => {
  router.push(path);
};

const toggleMenu = (index) => {
  toggle.value = !toggle.value;
  handle(sections.value[index].path);
};

const toggleModalAndMenu = () => {
  store.modalClick = !store.modalClick;
  toggle.value = !toggle.value;
};

const toggleModal = () => {
  store.modalClick = !store.modalClick;
};
</script>

<style scoped>
/* Your custom styles can go here */
</style>
