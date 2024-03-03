<script setup>
defineProps({
    message: {
        type: String,
        required: true,
    },
    isUser: {
        type: Boolean,
        required: true,
    },
    isLoading: {
        type: Boolean,
        required: false,
    },
});
</script>

<template>
    <div class="flex items-start gap-2.5 mb-4" :class="isUser ? ' flex-row-reverse' : ''">
        <img class="w-8 h-8 rounded-full"
            :src="isUser ? '/src/assets/user.png' : '/src/assets/pixlr-image-generator-51abc63a-2494-4e5f-8bf8-e3e8704617cd.png'"
            alt="Jese image">
        <l-bouncy size="45" speed="1.75" color="black" v-if="isLoading"></l-bouncy>
        <div class="flex flex-col w-full max-w-2xl leading-1.5 p-4 border-gray-200"
            :class="isUser ? 'rounded-s-xl rounded-ee-xl bg-blue-800' : 'rounded-e-xl rounded-es-xl bg-gray-600'" v-else>
            <div class="flex items-center space-x-2 rtl:space-x-reverse">
                <span class="text-sm font-semibold text-gray-900 dark:text-white">{{ isUser ? 'You' : 'Analyzer'
                    }}</span>
            </div>
            <p class="text-sm font-normal py-2.5 text-gray-900 dark:text-white">{{ message }}</p>
        </div>
    </div>
</template>