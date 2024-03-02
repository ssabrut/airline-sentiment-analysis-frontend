<script setup>
import { Pinecone } from '@pinecone-database/pinecone';
import { onMounted, ref } from 'vue';

import Navigation from './components/Navigation.vue';
import Input from './components/Input.vue';
import Bubble from './components/Bubble.vue';

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
      <Bubble />
    </div>
    <div>
      <Input />
    </div>
  </main>
</template>