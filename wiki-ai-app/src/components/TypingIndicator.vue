<template>
  <div class="flex space-x-1" aria-label="Loading">
    <span class="w-2 h-2 bg-gray-500 rounded-full animate-bounce" :style="style(0)"></span>
    <span class="w-2 h-2 bg-gray-500 rounded-full animate-bounce" :style="style(150)"></span>
    <span class="w-2 h-2 bg-gray-500 rounded-full animate-bounce" :style="style(300)"></span>
  </div>
</template>

<script setup>
const style = (delay) => ({ animationDelay: `${delay}ms` })
</script>

<style scoped>
@keyframes bounce {
  0%, 80%, 100% { transform: scale(0); }
  40% { transform: scale(1); }
}
.animate-bounce {
  animation: bounce 1.4s infinite;
}
</style>
