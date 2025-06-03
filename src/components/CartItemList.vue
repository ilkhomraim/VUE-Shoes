<script setup>
import { inject } from 'vue'
import CartItem from './CartItem.vue'

const { cart, removeFromCart } = inject('cart')

const emit = defineEmits(['addToFavorite', 'addToCart'])

defineProps({
  items: Array,
  isFavorite: Boolean,
})
</script>

<template>
  <div class="flex flex-col gap-5" v-auto-animate>
    <CartItem
      v-for="item in cart"
      :key="item.id"
      :title="item.title"
      :price="item.price"
      :imageUrl="item.imageUrl"
      :onClickFavorite="isFavorite ? null : () => emit('addToFavorite', item)"
      :onClickAdd="isFavorite ? null : () => emit('addToCart', item)"
      :isFavorite="item.isFavorite"
      :isAdded="item.isAdded"
      @on-click-remove="() => removeFromCart(item)"
    />
  </div>
</template>
