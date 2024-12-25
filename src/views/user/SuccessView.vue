<script setup>
import { ref, onMounted } from 'vue'
import UserLayout from '../../layouts/UserLayout.vue'

import { useCartStore } from '../../stores/user/cart'

const cartStore = useCartStore()
const orderData = ref({})

onMounted(() => {
  cartStore.loadCheckout()
  if (cartStore.checkout.orderNamder) {
    orderData.value = cartStore.checkout
  }
})
</script>

<template>
  <UserLayout>
    <div class="container mx-auto">
      <div class="container mx-auto max-w-2xl p-8 bg-base-100 my-4 border border-base-200 shadow-md">
        <div>
          <div class="text-2xl font-bold">Your order is successful!</div>
          <div>Hi {{ orderData.name }}</div>
          <div>Prepare to wait to receive the product.</div>
        </div>
        <div class="divider"></div>
        <div class="grid grid-cols-4 gap-2">
          <div>
            <div class="font-bold">Order date</div>
            <div>{{ orderData.createdDate }}.</div>
          </div>
          <div>
            <div class="font-bold">Order number</div>
            <div>{{ orderData.orderNamder }}</div>
          </div>
          <div>
            <div class="font-bold">Payment method</div>
            <div>{{ orderData.PaymentMethod }}</div>
          </div>
          <div>
            <div class="font-bold">Address</div>
            <div>{{ orderData.address }}</div>
          </div>
        </div>
        <div class="divider"></div>
        <div v-for="product in orderData.products" :key="product" class="grid grid-cols-4 gap-2 items-center">
          <div>
            <img class="w-full" :src="product.imageUrl" />
          </div>
          <div>
            <b>{{ product.name }}</b>
          </div>
          <div>
            Quantity: {{ product.quantity }}
          </div>
          <div>
            Total price {{ product.price * product.quantity }}
          </div>
        </div>
        <div class="divider"></div>
        <div class="flex justify-between">
          <div class="font-bold">All product prices</div>
          <div>{{ orderData.totalPrice }}</div>
        </div>
        <div class="flex justify-between mt-4">
          <div>Shipping cost</div>
          <div>30</div>
        </div>
        <div class="divider"></div>
        <div class="flex justify-between">
          <div>Total price</div>
          <div>{{ orderData.totalShipping }}</div>
        </div>
        <div class="divider"></div>
        <div>Thank you for purchasing our products.</div>
      </div>
    </div>
  </UserLayout>
</template>