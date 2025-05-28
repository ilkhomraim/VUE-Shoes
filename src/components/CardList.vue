<script setup>
import Card from './Card.vue'

defineProps({
  items: Array,
})

const emit = defineEmits(['addToFavorite'])

const onClickAdd = () => {
  emit('addToFavorite', item)
}
</script>

<template>
  <div class="grid grid-cols-4 gap-5 max-xl:grid-cols-3 max-md:grid-cols-2">
    <Card
      v-for="item in items"
      :key="item.id"
      :title="item.title"
      :id="item.id"
      :imageUrl="item.imageUrl"
      :price="item.price"
      :onClickFavorite="() => emit  ('addToFavorite', item)"
      :isFavorite="item.isFavorite"
    />
  </div>
</template>
