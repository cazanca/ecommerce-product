<template>
  <button
    @click="handleClick"
    class="flex items-center gap-4 justify-center bg-[var(--orange)] hover:bg-[var(--pale-orange)] capitalize text-sm w-full rounded-md py-3 px-4 font-semibold text-[var(--very-dark-grayish-blue)]"
  >
    <slot />
  </button>
</template>

<script setup>
const emit = defineEmits(['click'])

const handleClick = event => {
  emit('click', event)
}
</script>
