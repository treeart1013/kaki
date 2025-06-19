<template>
  <form @submit.prevent="onSend" class="p-4 border-t border-gray-700 flex">
    <textarea
      v-model="text"
      class="flex-grow bg-gray-800 text-gray-100 p-2 rounded mr-2 resize-none"
      rows="1"
      placeholder="메시지를 입력하세요"
      @keydown.enter.exact.prevent="onSend"
    ></textarea>
    <button type="submit" class="bg-blue-600 px-4 py-2 rounded">전송</button>
  </form>
</template>

<script setup>
import { ref } from 'vue'

const emit = defineEmits(['send'])

const text = ref('')

function onSend() {
  if (text.value.trim() === '') return
  emit('send', text.value)
  text.value = ''
}
</script>

<style scoped>
</style>
