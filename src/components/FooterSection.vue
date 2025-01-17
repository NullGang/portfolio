<script setup lang="ts">
const scrollToTop = () => {
  window.scrollTo({ top: 0, behavior: 'smooth' })
}
</script>

<template>
  <footer class="section-padding bg-dark/50">
    <div class="max-w-6xl mx-auto">
      <div class="flex flex-col md:flex-row justify-between items-center">
        <div class="text-light/60 mb-6 md:mb-0">
          © {{ new Date().getFullYear() }} NullOnRise. All rights reserved.
        </div>
        
        <div class="flex gap-6">
          <a href="/privacy" class="text-light/60 hover:text-light">Privacy Policy</a>
          <a href="/terms" class="text-light/60 hover:text-light">Terms of Service</a>
          <button @click="scrollToTop" class="text-light/60 hover:text-light">
            Back to Top ↑
          </button>
        </div>
      </div>
    </div>
  </footer>
</template>