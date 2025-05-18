<script setup>
import Header from './components/Header.vue'
import CardList from './components/CardList.vue'
import Drawer from './components/Drawer.vue'
</script>

<template>
  <!-- <Drawer /> -->
  <div class="bg-white w-4/5 m-auto rounded-xl shadow-xl mt-10">
    <Header />

    <div class="p-10">
      <div class="flex justify-between items-center mb-8">
        <h2 class="text-3xl font-bold">Все Кроссовки</h2>

        <select
          class="py-2 px-3 border border-gray-200 rounded-md outline focus:border-gray-300 transition outline-none"
        >
          <option>По названию</option>
          <option>По цене (дешевые)</option>
          <option>По цене (дорогие)</option>
        </select>

        <div class="relative">
          <img class="absolute left-3 top-3" src="/search.svg" alt="" />
          <input
            class="border border-gray-200 rounded-md py-2 pl-12 pr-4 outline-none focus:border-gray-300 transition"
            placeholder="Поиск"
          />
        </div>
      </div>

      <CardList />
    </div>
  </div>
</template>
<style scoped></style>
