<script setup>
import { ref } from 'vue';
const chatId = ref('')
const message = ref('')
const feedbackSend = ref(null)
const props =defineProps({
   token: String,
   url: String
})
const handleSendMessage = () => {
   fetch(`${props.url}${props.token}/sendMessage`, {
      method: 'POST',
      headers: {
         'Content-Type': 'application/json'
      },
      body: JSON.stringify({
         chat_id: chatId.value,
         text: message.value
      })
   })
   .then(data => {
      if(!data.ok) return feedbackSend.value = false
      feedbackSend.value = true
      chatId.value = ''
      message.value = ''
   })
}
</script>
<template>
   <div class="w-full max-w-md bg-gray-800 text-white rounded-lg border border-gray-700">
      <div class="flex flex-col gap-4 p-4">
         <h1 class="text-2xl font-bold text-center">
            <span class="text-[#2aabee]">Test</span> messages
         </h1>
         <input type="text" placeholder="CHAT ID" class="bg-gray-700 border border-transparent focus:border-[#2aabee] text-white placeholder-gray-400 placeholder:text-center flex w-full rounded-md px-2 py-1 text-sm focus:outline-none disabled:cursor-not-allowed disabled:opacity-50" v-model="chatId" />
         <textarea type="text" placeholder="MESSAGE" class="bg-gray-700 border border-transparent focus:border-[#2aabee] text-white placeholder-gray-400 placeholder:text-center flex items-center w-full rounded-md px-2 py-1 text-sm focus:outline-none disabled:cursor-not-allowed disabled:opacity-50" v-model="message" />
         <button type="submit" class="cursor-pointer w-full bg-[#2aabee] hover:bg-[#2aabee] text-white font-bold py-1 rounded transition-colors duration-300 text-sm" @click="handleSendMessage">
            Send Message
         </button>
         <span v-if="feedbackSend != null" class="font-semibold" :class="{ 'text-green-500': feedbackSend, 'text-red-500': !feedbackSend }">
            {{ feedbackSend ? 'Message sent' : 'Message not sent' }}
         </span>
      </div>
   </div>
</template>