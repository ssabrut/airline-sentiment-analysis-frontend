<script setup>
import { Pinecone } from '@pinecone-database/pinecone';
import { onMounted, ref } from 'vue';

import Navigation from './components/Navigation.vue';

const pinecone = ref(null);
const index = ref(null);

onMounted(async () => {
  pinecone.value = new Pinecone({apiKey: '7eb750c0-2b55-47f6-a3c0-cd7994703b21'});
  index.value = pinecone.value.index('airline-sentiment-analysis');
})
</script>

<template>
  <nav class="mb-16">
    <Navigation />
  </nav>
  <main class="container mx-auto">
    <div class="w-full mb-4 border border-gray-200 rounded-lg bg-gray-50">
      <div class="px-4 py-2.5 bg-white rounded-t-lg">
        <label for="comment" class="sr-only">Your comment</label>
        <textarea id="comment" rows="4"
          class="w-full px-0 text-sm text-gray-900 bg-white border-0 focus:ring-0 focus:border-0 "
          placeholder="Write a comment..." />
      </div>
      <div class="flex items-center justify-end px-3 py-2 border-t">
        <button type="submit"
          class="inline-flex items-center py-2.5 px-4 text-xs font-medium text-center text-white bg-blue-700 rounded-lg focus:ring-4 focus:ring-blue-200">
          Post comment
        </button>
      </div>
    </div>
  </main>
</template>