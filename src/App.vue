<script setup>
import { Pinecone } from '@pinecone-database/pinecone';
import { onMounted, ref, watch } from 'vue';

import Navigation from './components/Navigation.vue';
import Bubble from './components/Bubble.vue';

const pinecone = ref(null);
const index = ref(null);
const histories = ref([]);
const comment = ref('');
const errorState = ref(false);

onMounted(async () => {
  pinecone.value = new Pinecone({ apiKey: import.meta.env.VITE_PINECONE_API_KEY });
  index.value = pinecone.value.index(import.meta.env.VITE_PINECONE_INDEX);
  histories.value.push({
    message: 'Hello, I am Airline Sentiment Bot. Start Writing Your Comments and I will analyze them for you.',
    isUser: false,
  });
})

watch(comment, () => {
  errorState.value = false;
})

const postComment = async () => {
  if (comment.value.length === 0) {
    errorState.value = true;
    return;
  }

  histories.value.push({ message: comment.value, isUser: true });
  comment.value = '';
}
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
      <div class="w-full mb-1 border rounded-lg bg-gray-50" :class="errorState ? 'border-red-300' : 'border-gray-200'">
        <form>
          <div class="px-4 py-2.5 bg-white rounded-t-lg">
            <label for="comment" class="sr-only">Your comment</label>
            <textarea id="comment" rows="4"
              class="w-full px-0 text-sm text-gray-900 bg-white border-0 focus:ring-transparent focus:border-transparent"
              placeholder="Write your comment here..." v-model="comment" />
          </div>
          <div class="flex items-center justify-end px-3 py-2.5 border-t">
            <button type="button"
              class="inline-flex items-center py-2.5 px-4 text-xs font-medium text-center text-white bg-blue-950 rounded-lg focus:ring-4 focus:ring-blue-200"
              :class="comment.length === 0 ? 'bg-gray-300' : 'bg-blue-950'" @click="postComment"
              :disabled="comment.length == 0">
              Post comment
            </button>
          </div>
        </form>
      </div>
      <span class="font-medium text-xs text-red-600" v-if="errorState">Comment Cannot be Empty!</span>
    </div>
  </main>
</template>