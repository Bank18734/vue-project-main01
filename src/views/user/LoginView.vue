<template>
    <div class="min-h-screen flex items-center justify-center bg-white dark:bg-gray-500 from-emerald-400 to-emerald-700 w-full">
      <div class="w-full max-w-md bg-white rounded-lg shadow-md p-6 justify-center ">
        <!-- Login Form -->
        <h2 class="text-2xl font-bold mb-4 ">เข้าสู่ระบบ Mark shop</h2>
        <!-- Username Input -->
        <div class="mb-4">
          <input
            v-model="username"
            id="username"
            type="text"
            placeholder="username"
            class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-yellow-500"
          />
        </div>
  
        <!-- Password Input -->
        <div class="mb-6">
          <input
            v-model="password"
            id="password"
            type="password"
            placeholder="password"
            class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-yellow-500"
          />
        </div>
  
        
        <!-- Error Message -->
        <p v-if="errorMessage" class="text-red-500">{{ errorMessage }}</p>
  
        <!-- Login Button -->
        <button
          :disabled="loading"
          @click="handleLogin"
          class="w-full bg-yellow-600 text-white py-2 rounded-lg font-semibold mb-4 hover:bg-yellow-700"
        >
          {{ loading ? "กำลังเข้าสู่ระบบ..." : "เข้าสู่ระบบ" }}
        </button>
      </div>
    </div>
  </template>
    
    <script>
    export default {
      name: 'AdminLg',
      data() {
        return {
          username: '',
          password: '',
          errorMessage: '',
        };
      },
      methods: {
        handleLogin() {
          // ตรวจสอบข้อมูลการล็อกอิน (คุณสามารถเปลี่ยนให้เชื่อมต่อกับ API ได้)
          if (this.username === 'admin' && this.password === '123') {
            this.$router.push('/admin-dashboard'); // เปลี่ยนเส้นทางเมื่อเข้าสู่ระบบสำเร็จ
          } else {
            this.errorMessage = 'Invalid username or password';
          }
        },
      },
    };
    </script>
    