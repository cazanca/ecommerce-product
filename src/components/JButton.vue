<template>
  <button
    @click.prevent="handleClick"
    class="bg-[var(--orange)] text-[var(--very-dark-blue)] flex items-center justify-center py-2 gap-4 font-semibold rounded-md w-full hover:-translate-y-0.5 hover:drop-shadow-md active:translate-y-0 active:drop-shadow-sm"
  >
    <slot />
  </button>
</template>

<script setup>
const emit = defineEmits(['clickEvent'])

const handleClick = event => {
  emit('clickEvent', event)
}
</script>
