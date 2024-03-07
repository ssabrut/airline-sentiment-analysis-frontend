<script setup>
import { ref } from 'vue';

const dropdown = ref(false);
</script>

<template>
    <header>
        <nav class="border-gray-200 px-4 py-2 bg-blue-950">
            <div class="flex flex-wrap justify-between items-center mx-auto container">
                <a href="https://flowbite.com" class="flex items-center">
                    <span class="self-center text-xl font-semibold whitespace-nowrap dark:text-white">Airline Sentiment
                        Analyzer</span>
                </a>
                <div class="flex items-center lg:order-2">
                    <div class="relative">
                        <button id="dropdownDefaultButton" data-dropdown-toggle="dropdown"
                            class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center inline-flex items-center"
                            type="button" @click="dropdown = !dropdown">Repositories<svg class="w-2.5 h-2.5 ms-3"
                                aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 10 6">
                                <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"
                                    stroke-width="2" d="m1 1 4 4 4-4" />
                            </svg>
                        </button>

                        <!-- Dropdown menu -->
                        <div id="dropdown" class="z-10 absolute bg-white divide-y divide-gray-100 rounded-lg shadow w-44"
                            v-if="dropdown">
                            <ul class="py-2 text-sm text-gray-700" aria-labelledby="dropdownDefaultButton">
                                <li>
                                    <a href="https://github.com/ssabrut/airline-sentiment-analysis-frontend" class="block px-4 py-2 hover:bg-gray-100">Front End</a>
                                </li>
                                <li>
                                    <a href="https://github.com/ssabrut/airline-sentiment-analysis-backend" class="block px-4 py-2 hover:bg-gray-100">Back End</a>
                                </li>
                                <li>
                                    <a href="https://github.com/ssabrut/airline-sentiment-analysis" class="block px-4 py-2 hover:bg-gray-100">Notebook</a>
                                </li>
                            </ul>
                        </div>
                    </div>
                </div>
            </div>
        </nav>
    </header>
</template>