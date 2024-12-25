<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'
import UserLayout from '../../layouts/UserLayout.vue'

import { useCartStore } from '../../stores/user/cart'

const router = useRouter()
const cartStore = useCartStore()

// ข้อมูลสินค้า
const product = {
  name: "CELINE",
  description: "เสื้อเท็ดดี้แจ็กเก็ตทรงคลาสสิก ผ้าวูล",
  price: 120000,
  oldPrice: 150000,
  image: "https://twicpics.celine.com/product-prd/images/large/2V56D896C.38NO_1_WIN22_V9.jpg?twic=v1/cover=1:1/resize-max=900",
  details: " ผ้าวูล 90% โพลีอะไมด์ 10% วัสดุรอง หนังแกะ 100% ซับในผ้าวิสโคส 100%แผ่นประดับรูปตัวอักษร ‘C’ บริเวณหน้าอกและด้านหลังทรงคลาสสิกปกเท็ดดี้สองสีกระเป๋าหนังเจาะแนวทแยงสีตัดกัน 2 ช่องแผ่นหนังสีตัดกันบนแถบบ่าและแขนเสื้อแต่งขอบผ้ายืดสองสีกระดุมกด 7 เม็ดผลิตในอิตาลี เป็นต้น",
};

// จำนวนสินค้า
const quantity = ref(1);


// ฟังก์ชัน
const addToCart = (product) => {
  console.log('Hello add to cart')
  console.log(product)
  cartStore.addToCart(product)
  alert(`เพิ่ม ${quantity.value} ชิ้นของ "${product.name}" ลงในตะกร้าแล้ว!`);
};

const buyNow = (product) => {
  cartStore.addToCart(product)
  router.push({ name: 'cart' })
  alert("คุณเลือกซื้อสินค้าเรียบร้อยแล้ว!");
};
</script>

<template>
    <UserLayout>
        <div class="container mx-auto m-4">
            <div class="bg-gray-100 min-h-screen p-40">
                <div class="container mx-auto py-10">
                <div class="bg-white shadow-lg rounded-lg overflow-hidden">
                    <div class="flex flex-col md:flex-row">
                    <!-- Product Image -->
                    <div class="md:w-1/2">
                        <img :src="product.image" :alt="product.name" class="w-full h-auto object-cover">
                    </div>
                    <!-- Product Details -->
                    <div class="md:w-1/2 p-6 flex flex-col">
                        <h1 class="text-2xl font-bold text-gray-800">{{ product.name }}</h1>
                        <p class="mt-2 text-gray-600">{{ product.description }}</p>
                        <div class="mt-4">
                        <span class="text-xl font-semibold text-gray-800">฿{{ product.price }}</span>
                        <span v-if="product.oldPrice" class="text-sm line-through text-gray-400 ml-2">฿{{ product.oldPrice }}</span>
                        </div>
                        <div class="mt-4">
                        <label for="quantity" class="text-sm text-gray-600">จำนวน:</label>
                        <input
                            type="number"
                            id="quantity"
                            v-model="quantity"
                            min="1"
                            class="w-20 p-2 border border-gray-300 rounded-lg focus:ring-blue-500 focus:border-blue-500"
                        >
                        </div>
                        <button
                        @click="addToCart"
                        class="mt-6 bg-blue-500 text-white px-6 py-2 rounded-lg hover:bg-blue-600 focus:outline-none"
                        >
                        เพิ่มในตะกร้า
                        </button>
                        <button
                        @click="buyNow"
                        class="mt-4 bg-gray-100 text-gray-800 px-6 py-2 rounded-lg hover:bg-gray-200 focus:outline-none"
                        >
                        ซื้อเลย
                        </button>
                    </div>
                    </div>
                </div>
                <!-- Additional Product Info -->
                <div class="mt-10">
                    <h2 class="text-xl font-bold text-gray-800">รายละเอียดสินค้า</h2>
                    <p class="mt-2 text-gray-600">{{ product.details }}</p>
                </div>
                </div>
            </div>
        </div>
    </UserLayout>
</template>