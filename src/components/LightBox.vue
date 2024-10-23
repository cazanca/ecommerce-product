<template>
  <section
    v-if="isOpen"
    class="hidden bg-[var(--black-with-opacity)] z-20 absolute top-0 bottom-0 left-0 right-0 w-full h-screen items-center justify-center transition-all ease-in-out"
    :class="{ 'md:flex': isOpen }"
  >
    <div class="w-[400px] space-y-6">
      <div class="flex justify-end">
        <button
          class="text-white hover:text-[var(--orange)]"
          @click.prevent="emit('close-lightbox')"
        >
          <IconClose />
        </button>
      </div>
      <div class="lightbox-control">
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
              <img
                :src="slide.image"
                :alt="slide.alt"
                @click.prevent="emit('open-lightbox')"
                class="md:rounded-2xl cursor-pointer"
              />
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

          <!-- Carousel Indicators-->
          <div
            id="carousel-indicators"
            class="hidden md:flex items-center justify-center gap-6 mt-6"
          >
            <div v-for="(slide, index) in product.thumbnails" :key="index">
              <div
                :class="[
                  'relative rounded-lg h-[90px] cursor-pointer',
                  {
                    'opacity-70 border-2 border-[var(--orange)]':
                      currentSlide === index,
                  },
                ]"
              >
                <img
                  :src="slide.image"
                  :alt="slide.alt"
                  class="rounded-md h-full hover:opacity-70"
                  @click="goToSlide(index)"
                />
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import IconClose from './icons/IconClose.vue'
import IconNext from './icons/IconNext.vue'
import IconPrev from './icons/IconPrev.vue'
import { ref } from 'vue'

const props = defineProps({
  isOpen: {
    type: Boolean,
    required: true,
  },
  product: {
    type: Object,
    required: true,
  },
})

const emit = defineEmits(['close-lightbox'])

const currentSlide = ref(0)

const nextSlide = () => {
  currentSlide.value = (currentSlide.value + 1) % props.product.slides.length
}

const prevSlide = () => {
  currentSlide.value =
    (currentSlide.value - 1 + props.product.slides.length) %
    props.product.slides.length
}

const goToSlide = index => {
  currentSlide.value = index
}
</script>

<style scoped>
.carousel-control {
  @apply absolute top-1/2 -translate-y-[180%] bg-white cursor-pointer text-sm rounded-full w-8 h-8 flex items-center justify-center p-1;
}

.next {
  right: 0px;
}

.prev {
  left: 0px;
}
</style>
