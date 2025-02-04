<script setup>
defineProps(['infoMe', 'infoUpdates', 'noInfoMe', 'noInfoUpdates'])
</script>
<template>
   <Transition>
      <div class="w-full max-w-md bg-gray-800 text-white rounded-lg border border-gray-700">
         <div class="flex flex-col gap-2 p-2">
            <h1 class="text-2xl font-bold text-center">
               <span class="text-[#2aabee]">Bot</span> information
            </h1>
            <ul v-if="noInfoMe == null && infoMe != null">
               <li>
                  Bot ID: {{ infoMe.result.id }}
               </li>
               <li>
                  Name: {{ infoMe.result.first_name }}
               </li>
               <li>
                  Username:
                  <a :href="`https://t.me/${infoMe.result.username}`" target="_blank" class="underline">
                     {{ infoMe.result.username }}
                  </a>
               </li>
               <li>
                  Can Join Groups: {{ infoMe.result.can_join_groups ? 'Yes' : 'Not' }}
               </li>
            </ul>
            <span v-else class="w-full text-center italic">
               {{ noInfoMe }}
            </span>
            <h4 class="text-[#2aabee] font-semibold" v-if="noInfoUpdates == null && infoUpdates">Last Updates</h4>
            <code class="bg-gray-700 rounded p-2 text-xs whitespace-pre-wrap" v-if="noInfoUpdates == null && infoUpdates">
               {{ infoUpdates }}
            </code>
         </div>
      </div>
   </Transition>
</template>