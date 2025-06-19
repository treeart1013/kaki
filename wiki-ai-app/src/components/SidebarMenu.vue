<template>
  <aside class="w-56 h-full bg-gray-800 text-gray-100 flex flex-col p-4">
    <nav class="space-y-2">
      <button
        v-for="item in items"
        :key="item.label"
        class="flex items-center p-2 rounded hover:bg-gray-700"
        :class="{ 'bg-gray-700': active === item.label }"
        @click="active = item.label"
      >
        <span class="ml-2">{{ item.label }}</span>
      </button>
    </nav>
  </aside>
</template>

<script setup>
import { ref } from 'vue'

const items = [
  { label: '새 채팅' },
  { label: '프로젝트' },
  { label: '채팅 목록' },
  { label: '설정' }
]

const active = ref('새 채팅')
</script>

<style scoped>
</style>
