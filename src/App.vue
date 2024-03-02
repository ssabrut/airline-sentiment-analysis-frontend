<script setup>
import { Pinecone } from '@pinecone-database/pinecone';
import { onMounted, ref } from 'vue';

import Navigation from './components/Navigation.vue';
import Bubble from './components/Bubble.vue';

const pinecone = ref(null);
const index = ref(null);
const histories = ref([]);
const comment = ref('');

onMounted(async () => {
  pinecone.value = new Pinecone({ apiKey: import.meta.env.VITE_PINECONE_API_KEY });
  index.value = pinecone.value.index(import.meta.env.VITE_PINECONE_INDEX);
  histories.value.push({
    message: 'Hello, I am Airline Sentiment Bot. Start Writing Your Comments and I will analyze them for you.',
    isUser: false,
  });
  histories.value.push({
    message: 'Hello, I am Airline Sentiment Bot. Start Writing Your Comments and I will analyze them for you.',
    isUser: true,
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
      <div class="w-full mb-4 border border-gray-200 rounded-lg bg-gray-50">
        <div class="px-4 py-2.5 bg-white rounded-t-lg">
          <label for="comment" class="sr-only">Your comment</label>
          <textarea id="comment" rows="4"
            class="w-full px-0 text-sm text-gray-900 bg-white border-0 focus:ring-transparent focus:border-transparent" placeholder="Write your comment here..."
            v-model="comment" />
        </div>
        <div class="flex items-center justify-end px-3 py-2.5 border-t">
          <button type="submit"
            class="inline-flex items-center py-2.5 px-4 text-xs font-medium text-center text-white bg-blue-950 rounded-lg focus:ring-4 focus:ring-blue-200">
            Post comment
          </button>
        </div>
      </div>
    </div>
  </main>
</template>