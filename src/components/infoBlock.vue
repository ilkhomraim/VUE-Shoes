<script setup>
import { inject } from 'vue'

const { closeDrawer } = inject('cart')

defineProps({
  imageUrl: String,
  title: String,
  description: String,
})
</script>

<template>
  <div class="flex items-center flex-col text-center gap-1 w-72 mx-auto">
    <img height="120" width="120" :src="imageUrl" alt="" />
    <h2 class="mt-4 text-2xl font-bold">{{ title }}</h2>
    <p class="text-gray-400">{{ description }}</p>
    <button
      @click="closeDrawer"
      class="bg-lime-500 w-full rounded-xl py-4 font-medium opacity-80 mt-5 cursor-pointer text-white hover:bg-lime-600 transition active:bg-lime-700"
    >
      Вернуться назад
    </button>
  </div>
</template>
