<script setup>
import { ref, onMounted } from 'vue'
import UserLayout from '../../layouts/UserLayout.vue'

const profileImageUrl = ref('https://pbs.twimg.com/media/EseliMeWMAURwpi.jpg')
const email = ref('')
const name = ref('')

const handleFileUpload = (event) => {
  const file = event.target.files[0]

  if (file) {
    const reader = new FileReader()
    reader.onload = (e) => {
      profileImageUrl.value = e.target.result
    }
    reader.readAsDataURL(file)
  }
}

const updateProfile = () => {
  const profileData = {
    imageUrl: profileImageUrl.value,
    email: email.value,
    name: name.value
  }
  localStorage.setItem('profile-data', JSON.stringify(profileData))
  alert('Profile updated successfully!')
}

onMounted(() => {
  let profileData = localStorage.getItem('profile-data')
  if (profileData) {
    profileData = JSON.parse(profileData)
    profileImageUrl.value = profileData.imageUrl
    email.value = profileData.email
    name.value = profileData.name
  }
})
</script>

<template>
  <UserLayout>
    <div class="container mx-auto max-w-2xl p-4 bg-base-100 my-4 border border-base-200 shadow-md">
      <div class="text-2xl font-bold">Your Profile</div>

      <div class="flex flex-col items-center">
        <div class="flex flex-col items-center">
          <div class="avatar">
            <div class="w-24 rounded-full">
              <img :src="profileImageUrl"/>
            </div>
          </div>
          <label class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-900 mr-[185px]" for="file_input">Upload file</label>
          <input class="block w-full text-sm text-gray-900 border border-gray-300 rounded-lg cursor-pointer bg-gray-50 dark:text-gray-400 focus:outline-none dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400" aria-describedby="file_input_help" id="file_input" type="file" @change="handleFileUpload">
          <p class="mt-1 text-sm text-gray-500 dark:text-gray-900" id="file_input_help">SVG, PNG, JPG or GIF (MAX. 800x400px).</p>
        </div>
        <div class="grid gap-6 mb-4 w-full">
          <div>
              <label for="first_name" class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-900">Email</label>
              <input v-model="email" type="text" id="first_name" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="Type here" required />
          </div>
        </div>
        <div class="grid gap-6 mb-6 w-full">
          <div>
              <label for="first_name" class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-900">Name</label>
              <input v-model="name" type="text" id="first_name" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="Type here" required />
          </div>
        </div>
        <button @click="updateProfile" class="btn btn-primary w-full">Update Profile</button>
        </div>
      </div>
    </UserLayout>
</template>