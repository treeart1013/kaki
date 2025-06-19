<template>
  <div class="flex flex-col flex-1 overflow-y-auto p-4 space-y-4" ref="container">
    <div v-for="(msg, i) in messages" :key="i" class="flex" :class="msg.role === 'user' ? 'justify-end' : 'justify-start'">
      <div class="max-w-xl px-4 py-2 rounded-lg" :class="msg.role === 'user' ? 'bg-blue-600 text-white' : 'bg-gray-700 text-gray-100'">
        <HtmlRenderer :content="msg.content" />
      </div>
    </div>
    <div v-if="loading" class="flex justify-start">
      <div class="bg-gray-700 text-gray-100 px-4 py-2 rounded-lg">
        <TypingIndicator />
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, watch, nextTick } from 'vue'
import HtmlRenderer from './HtmlRenderer.vue'
import TypingIndicator from './TypingIndicator.vue'

const props = defineProps({
  messages: { type: Array, default: () => [] },
  loading: { type: Boolean, default: false }
})

const container = ref(null)

watch(() => props.messages.length, () => {
  nextTick(() => container.value?.scrollTo(0, container.value.scrollHeight))
})
</script>

<style scoped>
</style>
