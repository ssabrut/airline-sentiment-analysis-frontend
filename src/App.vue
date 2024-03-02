<script setup>
import { Pinecone } from '@pinecone-database/pinecone';
import { onMounted, ref } from 'vue';

import Navigation from './components/Navigation.vue';
import Input from './components/Input.vue';
import Bubble from './components/Bubble.vue';

const pinecone = ref(null);
const index = ref(null);
const histories = ref([]);

onMounted(async () => {
  pinecone.value = new Pinecone({ apiKey: import.meta.env.VITE_PINECONE_API_KEY });
  index.value = pinecone.value.index(import.meta.env.VITE_PINECONE_INDEX);
  histories.value.push({
    message: 'Hello, I am Airline Sentiment Bot. Start Writing Your Comments and I will analyze them for you.',
    isUser: false,
  });
})
</script>

<template>
  <nav class="mb-16">
    <Navigation />
  </nav>
  <main class="container mx-auto">
    <div class="mb-8">
      <Bubble v-for="history in histories" :isUser="history.isUser" :message="history.message" />
    </div>
    <div>
      <Input />
    </div>
  </main>
</template>