<script setup>
const emit = defineEmits(['onClickRemove'])

defineProps({
  id: Number,
  title: String,
  imageUrl: String,
  price: Number,
})
</script>

<template>
  <div
    class="flex border items-center border-slate-100 p-4 rounded-xl hover:border-slate-300 transition gap-5"
  >
    <img class="w-30" :src="imageUrl" :alt="title" />

    <div class="flex flex-col justify-between w-full">
      <p>{{ title }}</p>

      <div class="flex justify-between mt-2">
        <b>{{ price }} руб.</b>
        <img
          @click="emit('onClickRemove')"
          class="opacity-40 hover:opacity-100 cursor-pointer transition"
          src="/close.svg"
          alt=""
        />
      </div>
    </div>
  </div>
</template>
