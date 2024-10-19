<template>
  <!-- <header class="flex items-center h-24 border-b border-[var(--light-grayish-blue)]">
    <nav class="flex items-center justify-between w-full">
      <div class="flex items-center justify-between gap-x-14">
        <div>
          <img src="/images/logo.svg" alt="Sneakers Logo" />
        </div>
        <ul class="flex items-center gap-x-8">
          <li>
            <a href="#">Collections</a>
          </li>
          <li>
            <a href="#">Men</a>
          </li>
          <li>
            <a href="#">Women</a>
          </li>
          <li>
            <a href="#">About</a>
          </li>
          <li>
            <a href="#">Contact</a>
          </li>
        </ul>
      </div>
      <div class="flex items-center gap-x-8">
        <IconCart />
        <div class="w-[50px]">
          <img src="/images/image-avatar.png" class="w-full" alt="avatar" />
        </div>
      </div>
    </nav>
  </header> 
-->
  <header
    class="flex items-center py-4 px-6 border-b border-[var(--light-grayish-blue)] md:p-0 md:h-24"
  >
    <nav class="w-full flex items-center justify-between">
      <div class="flex items-center gap-x-6 md:gap-x-14">
        <button class="md:hidden" @click.prevent="isOpen = true">
          <IconMenu />
        </button>
        <div class="pb-1 md:pb-0">
          <img src="/images/logo.svg" alt="Sneakers logo" />
        </div>
        <div
          class="w-screen h-screen z-10 absolute inset-0 bg-[var(--black-with-opacity)] md:flex md:items-center md:relative md:h-full md:z-0 md:w-auto md:bg-transparent"
          :class="{ hidden: !isOpen }"
        >
          <ul
            class="h-screen w-56 bg-white p-4 px-6 space-y-4 font-semibold md:font-normal md:text-[var(--dark-grayish-blue)] md:h-auto md:w-auto md:flex md:items-center md:gap-x-8 md:space-y-0 md:p-0 md:bg-transparent md:mt-1"
          >
            <li class="mb-8 md:hidden">
              <button>
                <IconClose @click.prevent="isOpen = false" />
              </button>
            </li>
            <li v-for="(item, index) in menu" :key="index">
              <a href="#">{{ item }}</a>
            </li>
          </ul>
        </div>
      </div>
      <div class="flex items-center gap-x-6">
        <IconCart />
        <div class="w-[30px] md:w-[50px]">
          <img src="/images/image-avatar.png" class="w-full" alt="avatar" />
        </div>
      </div>
    </nav>
  </header>
  <main>Main</main>
</template>

<script setup>
import IconCart from './components/icons/IconCart.vue'
import IconMenu from './components/icons/IconMenu.vue'
import IconClose from './components/icons/IconClose.vue'
import { ref } from 'vue'

const isOpen = ref(false)
const menu = ['Collections', 'Men', 'Women', 'About', 'Contact']
</script>

<style>
#app {
  max-width: 1200px;
  margin: auto;
}
</style>
