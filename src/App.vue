<template>
  <Navbar @toggle-cart="toggleCart" :cart-length="cart.length" />
  <Cart :is-open="isCartOpen" :cart="cart" @remove-item="removeFromCart" />
  <ProductDisplay
    :product="product"
    :quantity="quantity"
    @increment="increment"
    @decrement="decrement"
    @add-to-cart="addToCart(product)"
    @open-lightbox="openLightBox"
  />
  <LightBox
    :is-open="isLightBoxOpen"
    :product="product"
    @close-lightbox="closeLightBox"
  />
</template>

<script setup>
import { ref, provide } from 'vue'
import Navbar from './components/Navbar.vue'
import Cart from './components/Cart.vue'
import ProductDisplay from './components/ProductDisplay.vue'
import LightBox from './components/LightBox.vue'

const isCartOpen = ref(false)
const isLightBoxOpen = ref(false)
const cart = ref([])
const quantity = ref(1)

const increment = () => {
  quantity.value += 1
}

const decrement = () => {
  if (quantity.value > 1) {
    quantity.value -= 1
  } else {
    alert('You reach the minimum value required')
  }
}

const product = {
  company: 'Sneaker Company',
  name: 'Fall Limited Edition Sneakers',
  description:
    'These low-profile sneakers are your perfect casual wear companion. Featuring a durable rubber outer sole, they’ll withstand everything the weather can offer.',

  image: '/images/image-product-1-thumbnail.jpg',
  slides: [
    { image: '/images/image-product-1.jpg', alt: 'Product 1' },
    { image: '/images/image-product-2.jpg', alt: 'Product 2' },
    { image: '/images/image-product-3.jpg', alt: 'Product 3' },
    { image: '/images/image-product-4.jpg', alt: 'Product 4' },
  ],
  thumbnails: [
    {
      image: '/images/image-product-1-thumbnail.jpg',
      alt: 'Product 1 thumbnail',
    },
    {
      image: '/images/image-product-2-thumbnail.jpg',
      alt: 'Product 2 thumbnail',
    },
    {
      image: '/images/image-product-3-thumbnail.jpg',
      alt: 'Product 3 thumbnail',
    },
    {
      image: '/images/image-product-4-thumbnail.jpg',
      alt: 'Product 4 thumbnail',
    },
  ],
  price: 250.0,
  discount: 0.5,
}

const toggleCart = () => {
  isCartOpen.value = !isCartOpen.value
}

const openLightBox = () => {
  isLightBoxOpen.value = true
}

const closeLightBox = () => {
  isLightBoxOpen.value = false
}

const closeCart = () => {
  isCartOpen.value === true ? (isCartOpen.value = false) : null
}

const addToCart = product => {
  const itemInCart = cart.value.find(item => item.id === product.id)
  /*
  if (itemInCart) {
    itemInCart.quantity++
  } else {
    cart.value.push({ ...product, quantity })
  }
*/
  if (!itemInCart) {
    cart.value.push({ ...product, quantity })
  }
}

const removeFromCart = product => {
  const index = cart.value.findIndex(item => item.id === product.id)

  if (index !== -1) {
    // se o item estiver no carrinho
    cart.value.splice(index, 1)
    /*if (cart.value[index].quantity > 1) {
      cart.value[index].quantity--
    } else {
      cart.value.splice(index, 1)
    }*/
  }
}

provide('closeCart', closeCart)
</script>
