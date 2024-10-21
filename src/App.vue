<template>
  <header
    class="flex items-center py-4 px-6 border-b-2 border-[var(--light-grayish-blue)] md:p-0 md:h-24"
  >
    <nav class="w-full flex items-center justify-between">
      <div class="flex items-center gap-x-6 md:gap-x-14">
        <button class="md:hidden" @click.prevent="openMenu">
          <IconMenu />
        </button>
        <div class="pb-1 md:pb-0">
          <img src="/images/logo.svg" alt="Sneakers logo" />
        </div>
        <div
          class="w-screen h-screen z-10 absolute inset-0 bg-[var(--black-with-opacity)] md:flex md:items-center md:relative md:h-full md:z-0 md:w-auto md:bg-transparent"
          :class="{ hidden: !isMenuOpen }"
        >
          <ul
            class="h-screen w-56 bg-white p-4 px-6 space-y-4 font-semibold md:font-normal md:text-[var(--dark-grayish-blue)] md:h-auto md:w-auto md:flex md:items-center md:gap-x-8 md:space-y-0 md:p-0 md:bg-transparent md:mt-1"
          >
            <li class="mb-8 md:hidden">
              <button>
                <IconClose @click.prevent="isMenuOpen = false" />
              </button>
            </li>
            <li v-for="(item, index) in menu" :key="index">
              <a href="#">{{ item }}</a>
            </li>
          </ul>
        </div>
      </div>
      <div class="flex items-center gap-x-6 relative">
        <button class="relative flex items-center justify-center" @click.prevent="isCartOpen = !isCartOpen">
          <span v-if="cart.length" class="absolute -top-1 right-0 inline-block w-3.5 h-3.5 text-center text-white rounded-full text-[10px] font-semibold bg-[var(--orange)]">{{ cart.length }}</span>
          <IconCart/>
        </button>
        <div class="w-[30px] md:w-[50px] hover:border-2 rounded-full border-[var(--orange)]">
          <img src="/images/image-avatar.png" class="w-full " alt="avatar" />
        </div>

        <div v-if="isCartOpen" class="absolute z-10 top-14 right-0 w-[330px] bg-white drop-shadow-xl rounded-md md:-right-10">
          <div class="border-b-2 border-[var(--light-grayish-blue)] p-3">
            <h2 class="font-semibold">Cart</h2>
          </div>
          <div class="flex items-center justify-center min-h-28">
            <p class="text-sm text-[var(--dark-grayish-blue)] font-semibold">Your cart is empty</p>
          </div>
        </div>
      </div>
    </nav>
  </header>
  <main>

    <div class="relative w-full mx-auto overflow-hidden" id="carousel-container">
      <div id="carousel" class="flex transition-transform ease-in-out">
        <div v-for="(slide, index) in slides" :key="index" :class="['min-w-full transition-opacity  ease-in-out carousel-slide', {'opacity-100': currentSlide === index}]" v-show="currentSlide == index">
          <img :src="slide.image" :alt="slide.alt">
        </div>
      </div>

      <button @click.prevent="prevSlide" class="carousel-control prev">
        <IconPrev/>
      </button>
      <button @click.prevent="nextSlide" class="carousel-control next">
        <IconNext class="w-3"/>
      </button>
    </div>

    <div class="py-4 px-6">
      <h3 class="text-xs tracking-wider uppercase font-semibold  text-[var(--dark-grayish-blue)]">Sneaker Company</h3>
      <h1 class="mt-2 text-[var(--very-dark-grayish-blue)] text-3xl tracking-wide font-bold">Fall Limited Edition Sneakers</h1>
      <p class="mt-2 text-[var(--dark-grayish-blue)]">These low-profile sneakers are your perfect casual wear companion. Featuring a 
        durable rubber outer sole, they’ll withstand everything the weather can offer.</p>
    </div>
   </main>
</template>

<script setup>
import IconCart from './components/icons/IconCart.vue'
import IconMenu from './components/icons/IconMenu.vue'
import IconClose from './components/icons/IconClose.vue'
//import Button from './components/Button.vue'

import { onMounted, ref } from 'vue'
import IconPrev from './components/icons/IconPrev.vue'
import IconNext from './components/icons/IconNext.vue'

const isMenuOpen = ref(false)
const isCartOpen = ref(false)
const cart = []
const menu = ['Collections', 'Men', 'Women', 'About', 'Contact']

const openMenu = () => {
  isMenuOpen.value = true
  isCartOpen.value = false
}

const slides = [{image: '/images/image-product-1.jpg', alt: 'Product 1'}, {image: '/images/image-product-2.jpg', alt: 'Product 2'}, {image: '/images/image-product-3.jpg', alt: 'Product 3'}, {image: '/images/image-product-4.jpg', alt: 'Product 4'}]


const currentSlide = ref(0)

const nextSlide = () => {
  currentSlide.value = (currentSlide.value + 1) % slides.length 
}

const prevSlide = () => {
  currentSlide.value = (currentSlide.value - 1 + slides.length) % slides.length
}

onMounted(() => {
  setInterval(()=> {nextSlide()}, 5000)
})
/* 
const goToSlide = (index) => {
  currentSlide.value = index
}
 */</script>

<style>
#app {
  max-width: 1200px;
  margin: auto;
}

.carousel-control {
  @apply absolute top-1/2 bg-white cursor-pointer text-sm rounded-full w-8 h-8 flex items-center justify-center p-1
}

.next {
  right: 10px;
}

.prev {
  left: 10px;
}
</style>
