<template>
  <header
    class="flex items-center py-4 px-6 border-b-2 border-[var(--light-grayish-blue)] md:p-0 md:h-24"
  >
    <nav class="w-full flex items-center justify-between">
      <div class="flex items-center gap-x-6 md:gap-x-14">
        <button
          class="md:hidden text-[var(--dark-grayish-blue)]"
          @click.prevent="openMenu"
        >
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
              <button class="text-[var(--dark-grayish-blue)]">
                <IconClose @click.prevent="isMenuOpen = false" />
              </button>
            </li>
            <li v-for="(item, index) in menu" :key="index">
              <a href="#">{{ item }}</a>
            </li>
          </ul>
        </div>
      </div>
      <!-- Cart and Avatar Icon -->

      <div class="flex items-center gap-x-6 relative">
        <button
          class="relative flex items-center justify-center text-[var(--dark-grayish-blue)] hover:text-[var(--text-black)]"
          @click.prevent="emit('toggle-cart')"
        >
          <span
            v-if="cartLength"
            class="absolute -top-1 right-0 inline-block w-3.5 h-3 text-center text-white rounded-full text-[10px] font-semibold bg-[var(--orange)]"
            >{{ cartLength }}</span
          >
          <IconCart />
        </button>
        <div
          class="w-[30px] md:w-[50px] hover:border-2 rounded-full border-[var(--orange)]"
        >
          <img src="/images/image-avatar.png" class="w-full" alt="avatar" />
        </div>
      </div>
    </nav>
  </header>
</template>

<script setup>
import { ref, inject } from 'vue'
import IconMenu from './icons/IconMenu.vue'
import IconClose from './icons/IconClose.vue'
import IconCart from './icons/IconCart.vue'

const closeCart = inject('closeCart')

const isMenuOpen = ref(false)

const menu = ['Collections', 'Men', 'Women', 'About', 'Contact']

const openMenu = () => {
  isMenuOpen.value = true
  // close cart
  closeCart()
}

defineProps({
  cartLength: {
    type: Number,
    required: true,
  },
})

const emit = defineEmits(['toggle-cart'])
</script>
