<script setup>
import { ref } from 'vue'
import SidebarMenu from './components/SidebarMenu.vue'
import ChatHeader from './components/ChatHeader.vue'
import ChatWindow from './components/ChatWindow.vue'
import ChatInput from './components/ChatInput.vue'

const messages = ref([])
const loading = ref(false)

async function sendMessage(text) {
  messages.value.push({ role: 'user', content: text })
  loading.value = true
  try {
    const controller = new AbortController()
    const res = await fetch(`/agent/test?prompt=${encodeURIComponent(text)}&uuid=1&model=gpt-4`, {
      headers: { Accept: 'text/event-stream' },
      signal: controller.signal
    })
    const reader = res.body.getReader()
    let aiMessage = { role: 'assistant', content: '' }
    messages.value.push(aiMessage)

    const decoder = new TextDecoder('utf-8')
    while (true) {
      const { value, done } = await reader.read()
      if (done) break
      const chunk = decoder.decode(value)
      if (chunk.includes('[DONE]')) break
      const match = chunk.match(/data: (.*)/)
      if (match) {
        aiMessage.content += match[1]
      }
    }
  } catch (e) {
    messages.value.push({ role: 'assistant', content: 'AI 응답을 불러올 수 없습니다. 관리자에게 문의하세요.' })
  } finally {
    loading.value = false
  }
}
</script>

<template>
  <div class="h-full flex">
    <SidebarMenu />
    <div class="flex flex-col flex-1 overflow-hidden">
      <ChatHeader />
      <ChatWindow :messages="messages" :loading="loading" />
      <ChatInput @send="sendMessage" />
    </div>
  </div>
</template>

<style scoped>
</style>
