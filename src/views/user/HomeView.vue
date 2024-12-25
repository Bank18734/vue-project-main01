<script setup>
import { RouterLink } from 'vue-router'
import UserLayout from '../../layouts/UserLayout.vue'

</script>

<template>
    <UserLayout>
      <div class="container mx-auto">
      <div class="hero h-[80vh] " style="background-image: url(https://png.pngtree.com/thumb_back/fh260/background/20240417/pngtree-polo-t-shirt-store-interior-shop-shelves-with-colored-fashion-cotton-image_15660845.jpg);">
        <div class="hero-overlay bg-opacity-60"></div>
        <div class="hero-content text-center">
        <div class="max-w-md">
          <h1 class="text-5xl font-bold text-white">Hello Again</h1>
           <p class="py-6 text-white">
            Welcome to Trending Shop, where every product tells a story. From handpicked items to the latest trends!
            </p>
            <RouterLink :to="{ name: 'productcart' }" class="btn btn-primary">Explore Our Products</RouterLink>
            </div>
          </div>
        </div>
        </div>
    </UserLayout>
</template>