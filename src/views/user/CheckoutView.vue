<script setup>
import { reactive } from 'vue'
import { RouterLink,useRouter } from 'vue-router'

import UserLayout from '../../layouts/UserLayout.vue'
import { useCartStore } from '../../stores/user/cart'

const FormData = [
  {
    name: 'Email address',
    field: 'email',
  },
  {
    name: 'Name',
    field: 'name',
  },
  {
    name: 'Address',
    field: 'address',
  },
  {
    name: 'Note',
    field: 'note',
  }
]

const router = useRouter()
const cartStore = useCartStore()

const userFormData = reactive({
  email: '',
  name: '',
  address: '',
  note: '',
})

const payment = () => {
  cartStore.placeorder(userFormData)
  router.push({ name: 'success' })
}
</script>

<template>
  <UserLayout>
    <div class="container mx-auto">
    <div class="flex">  
      <h1 class="text-3xl font-bold m-4">Checkout Cart</h1>
    </div>
    <div class="flex">
      <section class="flex-auto w-64 bg-base-200 p-4">
        <div>
        <div v-for="form in FormData" :key="form" class="grid gap-6 mb-6 md:grid-cols-1">
        <div>
            <label for="first_name" class="block mb-2 text-sm font-medium text-gray-900 ">{{ form.name }}</label>

            <textarea
              v-if="form.field === 'address'"
              class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
              placeholder="Address"
              v-model="userFormData[form.field]">
              
            </textarea>
            <input 
              v-else 
              type="text" 
              class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" 
              placeholder="Type here"
              v-model="userFormData[form.field]"/>
        </div>
        </div>
        <button @click="payment" class="btn btn-primary w-full mt-4">ชำระเงิน</button>
        </div>
      </section>
      <section class="flex-auto w-32 bg-gray-200 border-l-black border-2 p-4">
        <div v-for="item in cartStore.items" :key="item" class="flex ">
          <div class="flex-1">
            <img class="w-full p-8 " :src="item.imageUrl"/>
          </div>
          <div class="flex-1 ">
            <div class="flex flex-col justify-between h-full">
          <div>
            <div>{{ item.name }}</div>
            <div>{{ item.about }}</div>
            <div>จำนวน: {{ item.quantity }}</div>
            <div>ราคา: {{ item.price }}฿</div>
          </div>
            <RouterLink :to="{ name: 'cart' }" class="btn btn-outline btn-primary m-2 ring-1  w-1/2">Edit</RouterLink>
          </div>
          </div>
        </div>
        <div class="divider p-4"></div>
          <div class="p-4">
            <div class="text-xl font-bold">Order Summary</div>
            <div class="flex justify-between">
              <div>Total :</div>
              <div>{{ cartStore.summaryPrice }}</div>
            </div>
            <div class="flex justify-between">
              <div>Estimate Shipping :</div>
              <div>30</div>
            </div>
          </div>
          <div class="p-4">
          <div class="divider"></div>
          <div class="flex justify-between mb-4">
              <div>Subtotal :</div>
              <div>{{ cartStore.summaryShippingcost }}</div>
            </div>
          </div>
      </section>
    </div>
    </div>
  </UserLayout>
</template>
