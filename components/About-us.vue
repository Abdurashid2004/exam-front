<template>
  <div class="container mt-4 md:mt-20 ">
    <div class="grid md:grid-cols-2 md:gap-10">
      <div>
        <h2 class="text-[64px] text-primary font-bold max-md:text-[28px] mb-9">О компании</h2>
        <div
          v-for="(item, index) in statis"
          :key="index"
          class="rounded-[15px] bg-second md:p-8 p-6 flex flex-col md:gap-y-20 gap-[52px] md:w-[85%] cursor-pointer w-full mb-5"
        >
          <p class="text-[64px] text-primary font-bold">{{ item.number }}</p>
          <p class="text-primary text-2xl font-medium">{{ item.info }}</p>
        </div>
      </div>
      <div class="mt-8">
        <p
          v-for="(item, index) in parag"
          class="mb-10 text-[20px] text-primary leading-[30px] font-medium"
          :key="index"
        >
          {{ item }}
        </p>
      </div>
    </div>
  </div>
</template>

<script setup>
const statis = ref([
  {
    number: "170+",
    info: "Товаров",
  },
  {
    number: "1000+ ",
    info: "Довольных покупателей",
  },
  {
    number: "170+",
    info: "Товаров",
  },
]);

const parag = ref([
  "Интернет-магазин NORNLIGHT предлагает широкий ассортимент светильников для освещения вашего дома или офиса. У нас вы найдете разнообразные модели светильников, от современных и стильных до классических и элегантных. Мы предлагаем качественные и надежные светильники от лучших производителей, которые подарят вам комфорт и уют.",
  "Покупая светильники в нашем интернет-магазине, вы получаете отличное соотношение цены и качества. Мы осуществляем доставку по всей России, чтобы каждый клиент мог насладиться прекрасным светом и удобством покупки онлайн. Обратитесь к нам сегодня и превратите ваш дом в оазис тепла и света с NORNLIGHT!",
  "Интернет-магазин NORNLIGHT предлагает широкий ассортимент светильников для освещения вашего дома или офиса. У нас вы найдете разнообразные модели светильников, от современных и стильных до классических и элегантных. Мы предлагаем качественные и надежные светильники от лучших производителей, которые подарят вам комфорт и уют.",
  "Покупая светильники в нашем интернет-магазине, вы получаете отличное соотношение цены и качества. Мы осуществляем доставку по всей России, чтобы каждый клиент мог насладиться прекрасным светом и удобством покупки онлайн. Обратитесь к нам сегодня и превратите ваш дом в оазис тепла и света с NORNLIGHT!",
]);
</script>
