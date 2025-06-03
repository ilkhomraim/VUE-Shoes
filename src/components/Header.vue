<script setup>
const emit = defineEmits(['openDrawer'])

defineProps({
  totalPrice: Number,
})
</script>

<template>
  <header
    class="flex justify-between border-b border-slate-300 px-10 py-8 max-xl:flex-col items-center gap-8 max-sm:py-5 max-sm:px-0"
  >
    <RouterLink to="/">
      <div class="flex items-center gap-4">
        <img class="w-10" src="/logo.png" alt="logo" />
        <div>
          <h2 class="text-xl font-bold uppercase">Vue Shoes</h2>
          <p class="text-slate-400">VUE shop</p>
        </div>
      </div></RouterLink
    >

    <ul class="flex items-center gap-10 max-sm:gap-5">
      <li
        @click="() => emit('openDrawer')"
        class="flex items-center gap-3 text-gray-500 hover:text-black cursor-pointer"
      >
        <img src="/cart.svg" alt="" />
        <b class="max-sm:text-sm">{{ totalPrice }} руб.</b>
      </li>

      <RouterLink to="/favorites">
        <li class="flex items-center gap-3 text-gray-500 hover:text-black cursor-pointer">
          <img src="/heart.svg" alt="" />
          <span class="max-sm:text-sm">Закладки</span>
        </li></RouterLink
      >

      <li class="flex items-center gap-3 text-gray-500 hover:text-black cursor-pointer">
        <img src="/profile.svg" alt="" />
        <span class="max-sm:text-sm">Профиль</span>
      </li>
    </ul>
  </header>
</template>
