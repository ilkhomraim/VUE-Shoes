<script setup>
import { inject, ref, reactive, watch, onMounted } from 'vue'
import CardList from '../components/CardList.vue'
import axios from 'axios'
import debounce from 'lodash.debounce'

const { cart, addToCart, removeFromCart } = inject('cart')

const items = ref([])

const filters = reactive({
  sortBy: 'title',
  searchQuery: '',
})

const onClickAddPlus = (item) => {
  if (!item.isAdded) {
    addToCart(item)
  } else {
    removeFromCart(item)
  }
}

const onChangeSearchInput = debounce((event) => {
  filters.searchQuery = event.target.value
}, 400)

const addToFavorite = async (item) => {
  try {
    if (!item.isFavorite) {
      const obj = {
        item_id: item.id,
      }

      item.isFavorite = true

      const { data } = await axios.post(`https://fa3088e6425c2332.mokky.dev/favorites`, obj)

      item.favoriteId = data.id
    } else {
      item.isFavorite = false
      await axios.delete(`https://fa3088e6425c2332.mokky.dev/favorites/${item.favoriteId}`)
      item.favoriteId = null
    }
  } catch (err) {
    console.log(err)
  }
}

const onChangeSelect = (event) => {
  filters.sortBy = event.target.value
}

const fetchFavorites = async () => {
  try {
    const { data: favorites } = await axios.get(`https://fa3088e6425c2332.mokky.dev/favorites`)

    items.value = items.value.map((item) => {
      const favorite = favorites.find((favorite) => favorite.item_id === item.id)

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
      favoriteId: null,
      isAdded: false,
    }))
  } catch (err) {
    console.log(err)
  }
}

onMounted(async () => {
  const localCart = localStorage.getItem('cart')
  cart.value = localCart ? JSON.parse(localCart) : []

  await fetchItems()
  await fetchFavorites()

  items.value = items.value.map((item) => ({
    ...item,
    isAdded: cart.value.some((cartItem) => cartItem.id === item.id),
  }))
})

watch(filters, fetchItems)

watch(cart, () => {
  items.value = items.value.map((item) => ({
    ...item,
    isAdded: false,
  }))
})
</script>

<template>
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

  <CardList :items="items" @add-to-favorite="addToFavorite" @add-to-cart="onClickAddPlus" />
</template>
