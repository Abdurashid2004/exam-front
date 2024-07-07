<template>
  <div class="container md:py-[71px] max-md:pt-[60px]">
    <div class="flex w-full items-center md:mb-[71px] mb-[28] justify-between">
      <h4 class="text-primary font-bold text-[40px] max-md:text-[28px]">
        Только проверенные бренды
      </h4>
      <div class="flex gap-[10px] max-md:hidden items-center">
        <button
          class="text-2xl h-[26px] duration-300 w-[39px] group hover:opacity-100 active:bg-primary flex items-center justify-center border border-primary rounded-full opacity-50"
          @click="decreaseSpeed"
        >
          <span
            class="mb-1.5 group-hover:text-primary text-primary group-active:text-white"
            >&#8592;</span
          >
        </button>
        <button
          class="text-2xl h-[26px] w-[39px] duration-300 hover:opacity-100 group active:bg-primary flex items-center justify-center border border-primary rounded-full opacity-50"
          @click="increaseSpeed"
        >
          <span
            class="mb-1.5 group-hover:text-primary text-primary group-active:text-white"
            >&rarr;</span
          >
        </button>
      </div>
    </div>
    <div
      class="carousel-wrapper"
      :style="{ '--ani-speed': `${animationSpeed}s` }"
    >
      <div class="carousel">
        <div class="item" v-for="(item, index) in logos" :key="index">
          <img :src="item.src" :alt="item.alt" />
        </div>
        <div
          class="item"
          v-for="(item, index) in logos"
          :key="'duplicate-' + index"
        >
          <img :src="item.src" :alt="item.alt" />
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const logos = [
  { src: "/brand1.png", alt: "Brand 1" },
  { src: "/brand2.png", alt: "Brand 2" },
  { src: "/brand3.png", alt: "Brand 3" },
  { src: "/brand1.png", alt: "Brand 1" },
  { src: "/brand2.png", alt: "Brand 2" },
  { src: "/brand3.png", alt: "Brand 3" },
  { src: "/brand1.png", alt: "Brand 1" },
  { src: "/brand2.png", alt: "Brand 2" },
  { src: "/brand3.png", alt: "Brand 3" },
];

const animationSpeed = ref(30);

const increaseSpeed = () => {
  animationSpeed.value = Math.max(10, animationSpeed.value - 5);
};

const decreaseSpeed = () => {
  animationSpeed.value = Math.min(60, animationSpeed.value + 5);
};
</script>

<style scoped>
:root {
  --bg-clr: #64748b;
}

.carousel-wrapper {
  --width: 300px;
  --num-items: 9;

  width: 100%;
  overflow: hidden;
  position: relative;
}
.carousel-wrapper::before,
.carousel-wrapper::after {
  content: "";
  position: absolute;
  width: 100%;
  height: 100%;
  z-index: 1;
  top: 0;
}
.carousel-wrapper::before {
  left: 0;
  background-image: linear-gradient(
    to right,
    var(--bg-clr) 0%,
    transparent 100%
  );
}
.carousel-wrapper::after {
  right: 0;
  background-image: linear-gradient(
    to left,
    var(--bg-clr) 0%,
    transparent 100%
  );
}

.carousel {
  display: flex;
  align-items: center;
  animation: slide var(--ani-speed) linear infinite;
}
.item {
  flex: 1 0 var(--width);
  text-align: center;
  padding: 1rem;
}
.item > img {
  width: 100%;
  height: auto;
  max-height: 120px;
  object-fit: contain;
}

@keyframes slide {
  100% {
    transform: translateX(calc(var(--width) * var(--num-items) * -1));
  }
}
</style>
