<script setup>
import { ref } from 'vue';
import Information from './components/Information.vue';
import Messages from './components/Messages.vue';
const token = ref('')
const url = 'https://api.telegram.org/bot'
const optionSelected = ref(1)
const infoMe = ref(null)
const infoUpdates = ref(null)
const noInfoMe = ref(null)
const noInfoUpdates = ref(null)
const getMe = () => {
  const fullUrl = `${url}${token.value}/getMe`
  fetch(fullUrl, {
    method: 'GET',
  })
  .then(response => response.json())
  .then(data => {
    if(!data.ok) return noInfoMe.value = '¡Fail! Try another TOKEN'
    noInfoMe.value = null
    infoMe.value = data
  })
}
const getUpdates = () => {
  const fullUrl = `${url}${token.value}/getUpdates`
  fetch(fullUrl, {
    method: 'GET',
  })
  .then(response => response.json())
  .then(data => {
    if(!data.ok) return noInfoUpdates.value = 'Vuelta a intentarlo'
    noInfoUpdates.value = null
    infoUpdates.value = data
  })
}
const handleGet = () => {
  getMe()
  getUpdates()
}
</script>
<template>
  <section class="flex flex-col gap-4 items-center justify-center min-h-screen bg-gray-900 text-white py-4">
    <div class="w-full max-w-md bg-gray-800 text-white rounded-lg border border-gray-700">
      <div class="flex flex-col gap-3 p-3">
        <h1 class="text-2xl font-bold text-center">
          Enter your <span class="text-[#2aabee]">Telegram</span> BOT Token
        </h1>
        <input type="password" placeholder="INCLUDE YOUR TOKEN"
          class="bg-gray-700 border border-transparent focus:border-[#2aabee] text-white placeholder-gray-400 placeholder:text-center flex w-full rounded-md px-2 py-1 text-sm focus:outline-none disabled:cursor-not-allowed disabled:opacity-50"
          v-model="token" autocomplete="new-password" />
        <button type="submit"
          class="cursor-pointer w-full bg-[#2aabee] hover:bg-[#2aabee] text-white font-bold py-1 rounded transition-colors duration-300 text-sm"
          @click="handleGet">
          Get Data
        </button>
      </div>
    </div>
    <div
      class="w-full max-w-md inline-flex items-center justify-center rounded-lg bg-gray-800 p-1.5 gap-x-2 text-sm border border-gray-700">
      <button type="button" @click="()=>optionSelected = 1"
        class="w-full inline-flex items-center justify-center whitespace-nowrap rounded-md px-2 py-0.5 font-medium ring-offset-background transition-all cursor-pointer focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2 disabled:pointer-events-none disabled:opacity-50"
        :class="optionSelected == 1 ? 'bg-[#2aabee] shadow' : 'bg-gray-700'">
        Information
      </button>
      <button type="button" @click="()=>optionSelected = 2"
        class="w-full inline-flex items-center justify-center whitespace-nowrap rounded-md px-2 py-0.5 font-medium ring-offset-background transition-all cursor-pointer focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2 disabled:pointer-events-none disabled:opacity-50"
        :class="optionSelected == 2 ? 'bg-[#2aabee] shadow' : 'bg-gray-700'">
        Test Messages
      </button>
    </div>
    <Information :infoMe="infoMe" :infoUpdates="infoUpdates" :noInfoMe="noInfoMe" :noInfoUpdates="noInfoUpdates"
      v-if="optionSelected == 1" />
    <Messages v-if="optionSelected == 2" :token="token" :url="url" />
    <!-- <div class="bg-orange-400 p-1 w-full max-w-md h-fit relative z-0 overflow-hidden py-10">
      <Transition enter-active-class="transition-all duration-300"
        leave-active-class="transition-all duration-300" enter-from-class="-translate-x-full" enter-to-class="translate-x-0"
        leave-from-class="translate-x-0" leave-to-class="-translate-x-full">
        <div class="absolute z-10 inset-0 size-40 bg-red-500" v-show="optionSelected == 1">
        </div>
        <Information class="" :infoMe="infoMe" :infoUpdates="infoUpdates" v-show="optionSelected == 1" />
      </Transition>
      <Transition enter-active-class="transition-all duration-300"
        leave-active-class="transition-all duration-300" enter-from-class="translate-x-full" enter-to-class="translate-x-0"
        leave-from-class="-translate-x-0" leave-to-class="translate-x-full">
        <div class="absolute inset-0 size-44 bg-blue-500" v-show="optionSelected == 2">
        </div>
        <Messages class="" v-show="optionSelected == 2" />
      </Transition>
    </div> -->
  </section>
</template>
<style scoped>
</style>