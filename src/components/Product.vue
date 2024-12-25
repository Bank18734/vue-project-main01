<script setup>
import { defineProps } from 'vue'
import { RouterLink } from 'vue-router'

defineProps({
  products: Array,
  addToCart: Function
})

</script>
<template>
    <!-- Products shelf -->
     <div class="container mx-auto">
    <section class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-4 m-4">
      <div v-for="product in products" :key="product.id" class="card card-compact bg-base-100 w-full shadow-xl">
        <figure>
        <img
        class="w-full" :src="product.imageUrl"/>
        </figure>
        <div class="card-body">
          <h2 class="card-title">{{ product.name }}</h2>
          <p>{{ product.about.substring(0, 100) }}</p>
          <p class="font-bold">฿{{ product.price }}</p>
          <div class="card-actions justify-between">
            <RouterLink :to="{name:'productdetail'}" type="button" class="mt-2 px-3 py-2 text-xs font-medium text-center text-white bg-blue-700 rounded-lg hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">MORE DETAIL</RouterLink>
          <button class="btn btn-primary " @click="addToCart(product)">ADD TO CART</button>
            </div>
          </div>
        </div>
      </section>
    </div>
</template>