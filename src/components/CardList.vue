<script setup>
import Card from './Card.vue'
</script>

<template>
  <div class="grid grid-cols-4 gap-5">
    <Card
      title="Мужские Кроссовки Nike Blazer Mid Suede"
      imageUrl="/sneakers/sneakers-1.jpg"
      :price="12900"
      :is-favorite="true"
    />
  </div>
</template>
