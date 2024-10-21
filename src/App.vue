<template>
  <Navbar @toggle-cart="toggleCart" :cart-length="cart.length" />
  <Cart :is-open="isCartOpen" :cart="cart" @remove-item="removeFromCart" />
</template>

<script setup>
import { ref, provide } from 'vue'
import Navbar from './components/Navbar.vue'
import Cart from './components/Cart.vue'

const isCartOpen = ref(false)
const cart = ref(['', ''])

const toggleCart = () => {
  isCartOpen.value = !isCartOpen.value
}
const closeCart = () => {
  isCartOpen.value === true ? (isCartOpen.value = false) : null
}

const addToCart = product => {
  // se der erro, adicione .value no cart => exemplo cart.value.find o«e itemInCart.value.quantity
  const itemInCart = cart.value.find(item => item.id === product.id)

  if (itemInCart) {
    itemInCart.quantity++
  } else {
    cart.value.push({ ...product, quantity: 1 })
  }
}

const removeFromCart = product => {
  const index = cart.value.findIndex(item => item.id === product.id)

  if (index !== -1) {
    // se o item estiver no carrinho
    if (cart.value[index].quantity > 1) {
      cart.value[index].quantity--
    } else {
      cart.value.splice(index, 1)
    }
  }
}

provide('closeCart', closeCart)
</script>
