<script setup>
import { onMounted, ref, reactive, watch } from 'vue'
import axios from 'axios'

import Header from './components/Header.vue'
import CardList from './components/CardList.vue'
import Drawer from './components/Drawer.vue'

const items = ref([])

const filters = reactive({
  sortBy: 'title',
  searchQuery: '',
})
const onChangeSelect = (event) => {
  filters.sortBy = event.target.value
}

const onChangeSearchInput = (event) => {
  filters.searchQuery = event.target.value
}

const addToFavorite = async (item) => {
  item.isFavorite = true
}

const fetchFavorites = async () => {
  try {
    const { data: favorites } = await axios.get(`https://fa3088e6425c2332.mokky.dev/favorites`)

    items.value = items.value.map((item) => {
      const favorite = favorites.find((favorite) => favorite.productId === item.id)

      if (!favorite) {
        return item
      }

      return {
        ...item,
        isFavorite: true,
        favoriteId: favorite.id,
      }
    })
  } catch (err) {
    console.log(err)
  }
}

const fetchItems = async () => {
  try {
    const params = {
      sortBy: filters.sortBy,
    }

    if (filters.searchQuery) {
      params.title = `*${filters.searchQuery}*`
    }

    const { data } = await axios.get(`https://fa3088e6425c2332.mokky.dev/items`, {
      params,
    })

    items.value = data.map((obj) => ({
      ...obj,
      isFavorite: false,
      isAdded: false,
    }))
  } catch (err) {
    console.log(err)
  }
}

onMounted(async () => {
  await fetchItems()
  await fetchFavorites()
})

watch(filters, fetchItems)
</script>

<template>
  <!-- <Drawer /> -->
  <div class="bg-white m-auto rounded-xl shadow-xl">
    <Header />

    <div class="p-10 max-lg:p-5">
      <div class="flex justify-between items-center mb-8 max-md:flex-col gap-4">
        <h2 class="text-3xl font-bold max-lg:text-2xl">Все Кроссовки</h2>

        <select
          @change="onChangeSelect"
          class="py-2 px-3 border border-gray-200 rounded-md outline focus:border-gray-300 transition outline-none"
        >
          <option value="name">По названию</option>
          <option value="price">По цене (дешевые)</option>
          <option value="-price">По цене (дорогие)</option>
        </select>

        <div class="relative">
          <img class="absolute left-3 top-3" src="/search.svg" alt="" />
          <input
            @input="onChangeSearchInput"
            class="border border-gray-200 rounded-md py-2 pl-12 pr-4 outline-none focus:border-gray-300 transition"
            placeholder="Поиск"
          />
        </div>
      </div>

      <CardList :items="items" />
    </div>
  </div>
</template>
<style scoped></style>
