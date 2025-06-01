<script setup>
import DrawerHead from './DrawerHead.vue'
import CartItemList from './CartItemList.vue'

defineProps({
  totalPrice: Number,
  vatPrice: Number,
})
</script>

<template>
  <div>
    <div class="fixed top-0 left-0 h-full w-full bg-black z-10 opacity-70 mb-4"></div>

    <div class="bg-white w-96 h-full fixed right-0 top-0 z-20 p-7 flex flex-col">
      <DrawerHead />

      <div class="flex-1 overflow-y-auto pb-5">
        <CartItemList />
      </div>

      <div class="mt-auto">
        <div class="flex flex-col gap-3">
          <div class="flex gap-2">
            <span>Итого:</span>
            <div class="flex-1 border-b border-dashed border-gray-300"></div>
            <b>{{ totalPrice }} р.</b>
          </div>

          <div class="flex gap-2">
            <span>Налог 5%.</span>
            <div class="flex-1 border-b border-dashed border-gray-300"></div>
            <b>{{ vatPrice }} р.</b>
          </div>
        </div>

        <button
          disabled=""
          class="bg-lime-500 w-full rounded-xl py-3 mt-5 disabled:bg-slate-400 cursor-pointer text-white hover:bg-lime-600 transition active:bg-lime-700"
        >
          Оформить заказ
        </button>
      </div>
    </div>
  </div>
</template>
