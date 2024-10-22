<template>
  <article>
    <div
      class="relative w-full mx-auto overflow-hidden"
      id="carousel-container"
    >
      <div id="carousel" class="flex transition-transform ease-in-out">
        <div
          v-for="(slide, index) in product.slides"
          :key="index"
          :class="[
            'min-w-full transition-opacity  ease-in-out carousel-slide',
            { 'opacity-100': currentSlide === index },
          ]"
          v-show="currentSlide == index"
        >
          <img :src="slide.image" :alt="slide.alt" />
        </div>
      </div>

      <button
        @click.prevent="prevSlide"
        class="text-[var(--very-dark-grayish-blue)] carousel-control prev"
      >
        <IconPrev />
      </button>
      <button
        @click.prevent="nextSlide"
        class="text-[var(--very-dark-grayish-blue)] carousel-control next"
      >
        <IconNext class="w-3" />
      </button>
    </div>

    <div class="py-4 px-6">
      <h3
        class="text-xs tracking-wider uppercase font-semibold text-[var(--dark-grayish-blue)]"
      >
        {{ product.company }}
      </h3>
      <h1
        class="mt-2 text-[var(--very-dark-grayish-blue)] text-3xl tracking-wide font-bold"
      >
        {{ product.name }}
      </h1>
      <p class="mt-2 text-[var(--dark-grayish-blue)]">
        {{ product.description }}
      </p>
      <div class="flex mt-4 gap-4 items-center">
        <p class="text-xl font-bold">${{ product.price * product.discount }}</p>
        <p
          class="bg-black rounded text-white text-xs font-semibold px-2 py-0.5"
        >
          {{ product.discount * 100 }}%
        </p>
        <p
          class="ml-auto text-[var(--dark-grayish-blue)] line-through font-semibold text-sm"
        >
          ${{ product.price }}
        </p>
      </div>

      <div
        class="bg-[var(--light-grayish-blue)] rounded-md mt-6 p-2 px-4 flex items-center justify-between"
      >
        <button @click.prevent="emit('decrement')" class="text-[var(--orange)]">
          <IconMinus />
        </button>
        <p class="font-semibold">{{ quantity }}</p>
        <button @click.prevent="emit('increment')" class="text-[var(--orange)]">
          <IconPlus />
        </button>
      </div>
      <JButton class="mt-8" @click.prevent="emit('add-to-cart')">
        <IconCart />
        <p>Add to cart</p>
      </JButton>
    </div>
  </article>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import IconNext from './icons/IconNext.vue'
import IconPrev from './icons/IconPrev.vue'
import IconPlus from './icons/IconPlus.vue'
import IconMinus from './icons/IconMinus.vue'
import IconCart from './icons/IconCart.vue'

import JButton from './JButton.vue'

const props = defineProps({
  product: {
    type: Object,
    required: true,
  },
  quantity: {
    type: Number,
    required: true,
  },
})

const emit = defineEmits(['increment', 'decrement', 'add-to-cart'])

const currentSlide = ref(0)

const nextSlide = () => {
  currentSlide.value = (currentSlide.value + 1) % props.product.slides.length
}

const prevSlide = () => {
  currentSlide.value =
    (currentSlide.value - 1 + props.product.slides.length) %
    props.product.slides.length
}

onMounted(() => {
  setInterval(() => {
    nextSlide()
  }, 5000)
})
</script>

<style>
.carousel-control {
  @apply absolute top-1/2 bg-white cursor-pointer text-sm rounded-full w-8 h-8 flex items-center justify-center p-1;
}

.next {
  right: 10px;
}

.prev {
  left: 10px;
}
</style>
