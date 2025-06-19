<template>
  <div v-html="content" class="prose prose-invert max-w-none"></div>
</template>

<script setup>
defineProps({
  content: {
    type: String,
    default: ''
  }
})
</script>

<style scoped>
</style>
