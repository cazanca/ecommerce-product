<template>
  <div
    v-if="isOpen"
    class="absolute z-10 top-14 right-0 w-[330px] bg-white drop-shadow-xl rounded-md md:-right-10"
  >
    <div class="border-b-2 border-[var(--light-grayish-blue)] p-3">
      <h2 class="font-semibold">Cart</h2>
    </div>
    <div class="flex items-center justify-center min-h-28">
      <ul>
        <li v-for="(item, index) in cart" :key="index">
          <div>
            <img :src="item.img" :alt="item.name">
          </div>
          <div>
            <p>{{ item.name }}</p>
            <p>
              ${{ item.price }} x {{ item.quantity }}
              <strong>${{ item.price * item.quantity }}</strong>
            </p>
          </div>
          <button class="text-[var(--dark-grayish-blue)]" @click.prevent="emit('remove-item', item)">
            <IconDelete />
          </button>
        </li>
      </ul>
      <p
        v-show="!cart.length"
        class="text-sm text-[var(--dark-grayish-blue)] font-semibold"
      >
        Your cart is empty
      </p>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import IconDelete from './icons/IconDelete.vue'

defineProps({
  isOpen: {
    type: Boolean,
    required: true,
  },
  cart: {
    type: Array,
    required: true,
  },
})

const emit = defineEmits(['remove-item'])
</script>
