<script setup>
const props = defineProps({
  id: Number,
  title: String,
  imageUrl: String,
  price: Number,
  isFavorite: Boolean,
  isAdded: Boolean,
  onClickFavorite: Function,
  onClickAdd: Function,
})

const visibleFavoriteButton = Boolean(props.onClickAdd)
</script>

<template>
  <div
    class="relative bg-white border-slate-300 border-solid rounded-3xl p-8 cursor-pointer hover:-translate-y-2 hover:shadow-xl transition max-lg:p-6 max-sm:p-1"
  >
    <div>
      <img
        v-if="visibleFavoriteButton"
        @click="onClickFavorite"
        class="absolute top-8 left-8"
        :src="!isFavorite ? '/like-1.svg' : '/like-2.svg'"
        alt=""
      />
      <img :src="imageUrl" alt="Sneaker" />
      <p class="mt-2 max-md:text-base max-sm:text-sm">{{ title }}</p>
    </div>

    <div class="flex justify-between mt-5">
      <div class="flex flex-col">
        <span class="text-slate-500">Цена:</span>
        <span class="font-bold">{{ price }} руб.</span>
      </div>
      <img
        v-if="visibleFavoriteButton"
        @click="onClickAdd"
        :src="!isAdded ? '/plus.svg' : '/checked.svg'"
        alt=""
      />
    </div>
  </div>
</template>
