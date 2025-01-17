<script setup lang="ts">
import { ref } from 'vue'

const form = ref({
  name: '',
  email: '',
  message: ''
})

const errors = ref({
  name: '',
  email: '',
  message: ''
})

const validateEmail = (email: string) => {
  return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email)
}

const validateForm = () => {
  let isValid = true
  errors.value = {
    name: '',
    email: '',
    message: ''
  }

  if (!form.value.name.trim()) {
    errors.value.name = 'Name is required'
    isValid = false
  }

  if (!form.value.email.trim()) {
    errors.value.email = 'Email is required'
    isValid = false
  } else if (!validateEmail(form.value.email)) {
    errors.value.email = 'Invalid email format'
    isValid = false
  }

  if (!form.value.message.trim()) {
    errors.value.message = 'Message is required'
    isValid = false
  }

  return isValid
}

const handleSubmit = () => {
  if (validateForm()) {
    // Handle form submission
    console.log('Form submitted:', form.value)
  }
}
</script>

<template>
  <section id="contact" class="section-padding">
    <div class="max-w-3xl mx-auto">
      <h2 class="text-4xl font-bold mb-12 gradient-text text-center">Let's Connect</h2>
      
      <form @submit.prevent="handleSubmit" class="glass p-8 rounded-lg">
        <div class="mb-6">
          <label class="block text-sm font-medium mb-2">Name</label>
          <input
            v-model="form.name"
            type="text"
            class="w-full px-4 py-2 rounded-lg bg-dark/50 border border-white/20 focus:border-primary outline-none"
            :class="{ 'border-red-500': errors.name }"
          >
          <p v-if="errors.name" class="mt-1 text-sm text-red-500">{{ errors.name }}</p>
        </div>
        
        <div class="mb-6">
          <label class="block text-sm font-medium mb-2">Email</label>
          <input
            v-model="form.email"
            type="email"
            class="w-full px-4 py-2 rounded-lg bg-dark/50 border border-white/20 focus:border-primary outline-none"
            :class="{ 'border-red-500': errors.email }"
          >
          <p v-if="errors.email" class="mt-1 text-sm text-red-500">{{ errors.email }}</p>
        </div>
        
        <div class="mb-6">
          <label class="block text-sm font-medium mb-2">Message</label>
          <textarea
            v-model="form.message"
            rows="4"
            class="w-full px-4 py-2 rounded-lg bg-dark/50 border border-white/20 focus:border-primary outline-none"
            :class="{ 'border-red-500': errors.message }"
          ></textarea>
          <p v-if="errors.message" class="mt-1 text-sm text-red-500">{{ errors.message }}</p>
        </div>
        
        <button type="submit" class="btn w-full">Send Message</button>
      </form>
      
      <div class="mt-12 flex justify-center gap-6">
        <a href="https://github.com/NullGang" target="_blank" class="btn">
          GitHub
        </a>
        <a href="https://discord.com/users/927262698260029460" target="_blank" class="btn">
          Discord
        </a>
      </div>
    </div>
  </section>
</template>