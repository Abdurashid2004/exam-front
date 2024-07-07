<template>
  <div class="max-md:container">
    <div class="w-full md:flex justify-center">
      <div
        class="bg-second md:mx-[5%] max-md:px-[5%] mt-8 rounded-[25px] md:rounded-[30px] md:w-[1650px] md:h-[450px]"
      >
        <div class="md:container">
          <swiper
            spaceBetween="30"
            :centeredSlides="true"
            :pagination="true"
            :loop="true"
            :autoplay="{
              delay: 2500,
              disableOnInteraction: false,
            }"
            :modules="modules"
            class="mySwiper"
          >
            <swiper-slide v-for="(item, index) in 8" :key="index">
              <div
                class="flex max-md:flex-col-reverse md:gap-[199px] md:mb-[150px]"
              >
                <h1
                  class="md:text-[64px] text-[28px] md:mt-[64px] mt-[25px] max-md:mb-12 font-bold md:leading-[75px]"
                >
                  Скидка 15% на все подвесные светильники
                  <span
                    class="bg-primary inline-block rounded-full text-white px-[27px]"
                    >до 5 февраля</span
                  >
                </h1>
                <img
                  src="/header.png"
                  class="w-[35%] max-md:w-full md:mr-[66px]"
                  alt="Candle"
                />
              </div>
            </swiper-slide>
          </swiper>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { Swiper, SwiperSlide } from "swiper/vue";
import "swiper/css/navigation";
import "swiper/css";
import "swiper/css/pagination";
import { Autoplay, Pagination, Navigation } from "swiper/modules";

const modules = [Autoplay, Pagination, Navigation];
</script>
<style scoped>
.swiper {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: grab;
}
.swiper:active {
  cursor: grabbing;
}

.swiper-slide {
  display: flex;
  justify-content: center;
  align-items: center;
}
.swiper-pagination {
  position: absolute;
  right: 20px;
  bottom: 20px;
}
</style>
