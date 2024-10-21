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
        <button
          class="relative flex items-center justify-center"
          @click.prevent="isCartOpen = !isCartOpen"
        >
          <span
            v-if="cart.length"
            class="absolute -top-1 right-0 inline-block w-3.5 h-3.5 text-center text-white rounded-full text-[10px] font-semibold bg-[var(--orange)]"
            >{{ cart.length }}</span
          >
          <IconCart />
        </button>
        <div
          class="w-[30px] md:w-[50px] hover:border-2 rounded-full border-[var(--orange)]"
        >
          <img src="/images/image-avatar.png" class="w-full" alt="avatar" />
        </div>

        <div
          v-if="isCartOpen"
          class="absolute z-10 top-14 right-0 w-[330px] bg-white drop-shadow-xl rounded-md md:-right-10"
        >
          <div class="border-b-2 border-[var(--light-grayish-blue)] p-3">
            <h2 class="font-semibold">Cart</h2>
          </div>
          <div class="flex items-center justify-center min-h-28">
            <p class="text-sm text-[var(--dark-grayish-blue)] font-semibold">
              Your cart is empty
            </p>
          </div>
        </div>
      </div>
    </nav>
  </header>
  <main>
    <div
      class="relative w-full mx-auto overflow-hidden"
      id="carousel-container"
    >
      <div id="carousel" class="flex transition-transform ease-in-out">
        <div
          v-for="(slide, index) in slides"
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

      <button @click.prevent="prevSlide" class="carousel-control prev">
        <IconPrev />
      </button>
      <button @click.prevent="nextSlide" class="carousel-control next">
        <IconNext class="w-3" />
      </button>
    </div>

    <div class="py-4 px-6">
      <h3
        class="text-xs tracking-wider uppercase font-semibold text-[var(--dark-grayish-blue)]"
      >
        Sneaker Company
      </h3>
      <h1
        class="mt-2 text-[var(--very-dark-grayish-blue)] text-3xl tracking-wide font-bold"
      >
        Fall Limited Edition Sneakers
      </h1>
      <p class="mt-2 text-[var(--dark-grayish-blue)]">
        These low-profile sneakers are your perfect casual wear companion.
        Featuring a durable rubber outer sole, they’ll withstand everything the
        weather can offer.
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
        <button @click.prevent="decrement">
          <svg
            width="12"
            height="4"
            xmlns="http://www.w3.org/2000/svg"
            xmlns:xlink="http://www.w3.org/1999/xlink"
          >
            <defs>
              <path
                d="M11.357 3.332A.641.641 0 0 0 12 2.69V.643A.641.641 0 0 0 11.357 0H.643A.641.641 0 0 0 0 .643v2.046c0 .357.287.643.643.643h10.714Z"
                id="a"
              />
            </defs>
            <use fill="#FF7E1B" fill-rule="nonzero" xlink:href="#a" />
          </svg>
        </button>
        <p class="font-semibold">{{ quantity }}</p>
        <button @click.prevent="increment">
          <svg
            width="12"
            height="12"
            xmlns="http://www.w3.org/2000/svg"
            xmlns:xlink="http://www.w3.org/1999/xlink"
          >
            <defs>
              <path
                d="M12 7.023V4.977a.641.641 0 0 0-.643-.643h-3.69V.643A.641.641 0 0 0 7.022 0H4.977a.641.641 0 0 0-.643.643v3.69H.643A.641.641 0 0 0 0 4.978v2.046c0 .356.287.643.643.643h3.69v3.691c0 .356.288.643.644.643h2.046a.641.641 0 0 0 .643-.643v-3.69h3.691A.641.641 0 0 0 12 7.022Z"
                id="b"
              />
            </defs>
            <use fill="#FF7E1B" fill-rule="nonzero" xlink:href="#b" />
          </svg>
        </button>
      </div>
      <Button class="mt-8" @click="addToCart(product)">
        <svg class="" width="22" height="20" xmlns="http://www.w3.org/2000/svg">
          <path
            d="M20.925 3.641H3.863L3.61.816A.896.896 0 0 0 2.717 0H.897a.896.896 0 1 0 0 1.792h1l1.031 11.483c.073.828.52 1.726 1.291 2.336C2.83 17.385 4.099 20 6.359 20c1.875 0 3.197-1.87 2.554-3.642h4.905c-.642 1.77.677 3.642 2.555 3.642a2.72 2.72 0 0 0 2.717-2.717 2.72 2.72 0 0 0-2.717-2.717H6.365c-.681 0-1.274-.41-1.53-1.009l14.321-.842a.896.896 0 0 0 .817-.677l1.821-7.283a.897.897 0 0 0-.87-1.114ZM6.358 18.208a.926.926 0 0 1 0-1.85.926.926 0 0 1 0 1.85Zm10.015 0a.926.926 0 0 1 0-1.85.926.926 0 0 1 0 1.85Zm2.021-7.243-13.8.81-.57-6.341h15.753l-1.383 5.53Z"
            fill="text-black"
            fill-rule="nonzero"
          />
        </svg>
        <p>Add to cart</p>
      </Button>
    </div>
  </main>
</template>

<script setup>
import IconCart from './components/icons/IconCart.vue'
import IconMenu from './components/icons/IconMenu.vue'
import IconClose from './components/icons/IconClose.vue'
import Button from './components/Button.vue'
import { onMounted, ref } from 'vue'
import IconPrev from './components/icons/IconPrev.vue'
import IconNext from './components/icons/IconNext.vue'

const isMenuOpen = ref(false)
const isCartOpen = ref(false)

const quantity = ref(0)
const cart = ref([])
const menu = ['Collections', 'Men', 'Women', 'About', 'Contact']

const increment = () => {
  quantity.value += 1
}

const decrement = () => {
  if (quantity.value > 0) {
    quantity.value -= 1
  }
}

const addToCart = product => {
  if (quantity.value > 0) {
    cart.value.push(product)
    return
  }
}

const openMenu = () => {
  isMenuOpen.value = true
  isCartOpen.value = false
}

const product = {
  company: 'Sneaker Company',
  description:
    'These low-profile sneakers are your perfect casual wear companion. Featuring a durable rubber outer sole, they’ll withstand everything the weather can offer.',
  price: 250,
  discount: 0.5,
}

const slides = [
  { image: '/images/image-product-1.jpg', alt: 'Product 1' },
  { image: '/images/image-product-2.jpg', alt: 'Product 2' },
  { image: '/images/image-product-3.jpg', alt: 'Product 3' },
  { image: '/images/image-product-4.jpg', alt: 'Product 4' },
]

const currentSlide = ref(0)

const nextSlide = () => {
  currentSlide.value = (currentSlide.value + 1) % slides.length
}

const prevSlide = () => {
  currentSlide.value = (currentSlide.value - 1 + slides.length) % slides.length
}

onMounted(() => {
  setInterval(() => {
    nextSlide()
  }, 5000)
})
/* 
const goToSlide = (index) => {
  currentSlide.value = index
}
 */
</script>

<style>
#app {
  max-width: 1200px;
  margin: auto;
}

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
