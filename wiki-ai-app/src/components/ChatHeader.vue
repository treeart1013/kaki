<template>
  <header class="p-4 border-b border-gray-700 flex justify-between items-center">
    <h1 class="text-lg font-semibold">{{ model }}</h1>
    <select v-model="model" class="bg-gray-800 border-gray-600 text-gray-100 rounded">
      <option>gpt-4</option>
      <option>gpt-3.5-turbo</option>
    </select>
  </header>
</template>

<script setup>
import { ref } from 'vue'

const model = ref('gpt-4')
</script>

<style scoped>
</style>
