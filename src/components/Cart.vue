<template>
  <div
    v-if="isOpen"
    class="absolute z-10 top-20 right-5 w-[90%] md:w-[330px] bg-white drop-shadow-xl rounded-md md:top-20 md:right-20"
  >
    <div class="border-b-2 border-[var(--light-grayish-blue)] p-3">
      <h2 class="font-semibold">Cart</h2>
    </div>
    <div class="flex flex-col px-4 py-6">
      <ul class="w-full">
        <li
          v-for="(item, index) in cart"
          :key="index"
          class="w-full flex items-center justify-between"
        >
          <div class="w-12 h-12 rounded">
            <img :src="item.image" :alt="item.name" class="rounded" />
          </div>
          <div>
            <p class="text-[var(--dark-grayish-blue)]">{{ item.name }}</p>
            <p class="text-sm text-[var(--dark-grayish-blue)]">
              ${{ item.price }} x {{ item.quantity }}
              <strong class="text-black"
                >${{ item.price * item.quantity }}</strong
              >
            </p>
          </div>
          <button
            class="text-[var(--dark-grayish-blue)] hover:text-red-400"
            @click.prevent="emit('remove-item', item)"
          >
            <IconDelete />
          </button>
        </li>
      </ul>
      <JButton v-if="cart.length" class="mt-6"> Checkout </JButton>
      <p
        v-show="!cart.length"
        class="text-center text-sm py-4 text-[var(--dark-grayish-blue)] font-semibold"
      >
        Your cart is empty
      </p>
    </div>
  </div>
</template>

<script setup>
import IconDelete from './icons/IconDelete.vue'
import JButton from './JButton.vue'

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
