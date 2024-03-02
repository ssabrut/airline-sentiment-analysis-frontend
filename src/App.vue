<script setup>
import { Pinecone } from '@pinecone-database/pinecone';
import { onMounted, ref } from 'vue';

import Navigation from './components/Navigation.vue';
import Input from './components/Input.vue';

const pinecone = ref(null);
const index = ref(null);

onMounted(async () => {
  pinecone.value = new Pinecone({ apiKey: '7eb750c0-2b55-47f6-a3c0-cd7994703b21' });
  index.value = pinecone.value.index('airline-sentiment-analysis');
})
</script>

<template>
  <nav class="mb-16">
    <Navigation />
  </nav>
  <main class="container mx-auto">
    <div class="mb-8">
      <div class="flex items-start gap-2.5">
        <div
          class="flex flex-col w-full max-w-[320px] leading-1.5 p-4 border-gray-200 bg-blue-950 rounded-e-xl rounded-es-xl">
          <div class="flex items-center space-x-2 rtl:space-x-reverse">
            <span class="text-sm font-semibold text-gray-900 dark:text-white">Bonnie Green</span>
            <span class="text-sm font-normal text-gray-500 dark:text-gray-400">11:46</span>
          </div>
          <p class="text-sm font-normal py-2.5 text-gray-900 dark:text-white">That's awesome. I think our users will
            really appreciate the improvements.</p>
          <span class="text-sm font-normal text-gray-500 dark:text-gray-400">Delivered</span>
        </div>
      </div>
    </div>
    <div>
      <Input />
    </div>
  </main>
</template>