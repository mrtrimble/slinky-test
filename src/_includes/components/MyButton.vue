<template>
  <button :class="color">
    <slot></slot>
  </button>
</template>

<script setup>
  const props = defineProps({
    color:{
      type: String,
      default: 'blue'
    }
  })
</script>