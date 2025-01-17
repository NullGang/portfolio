<script setup lang="ts">
import { onMounted, ref } from 'vue'
import gsap from 'gsap'
import { ScrollToPlugin } from 'gsap/ScrollToPlugin'

gsap.registerPlugin(ScrollToPlugin)

const title = ref<HTMLElement | null>(null)

onMounted(() => {
  if (title.value) {
    gsap.from(title.value, {
      y: 100,
      opacity: 0,
      duration: 1,
      ease: 'power4.out'
    })
  }
})

const scrollToAbout = () => {
  const aboutSection = document.getElementById('about')
  if (aboutSection) {
    gsap.to(window, {
      duration: 1.5,
      scrollTo: {
        y: aboutSection,
        offsetY: 0
      },
      ease: 'expo.inOut'
    })
  }
}
</script>

<template>
  <section class="min-h-screen flex items-center justify-center relative overflow-hidden section-padding" id="top">
    <div class="absolute inset-0 bg-gradient-to-br from-primary/20 to-secondary/20 animate-gradient"></div>
    
    <div class="relative z-10 text-center">
      <h1 ref="title" class="text-6xl md:text-8xl font-bold mb-6 gradient-text">
        NullOnRise
      </h1>
      <p class="text-xl md:text-2xl mb-8 text-light/80">
        Full Stack Developer & UI/UX Enthusiast
      </p>
      <button @click="scrollToAbout" class="btn btn-primary animate-float">
        Explore My Work
      </button>
    </div>
    
    <div class="absolute bottom-8 left-1/2 -translate-x-1/2 animate-bounce">
      <button @click="scrollToAbout" class="text-light/60 hover:text-light">
        <svg class="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 14l-7 7m0 0l-7-7m7 7V3" />
        </svg>
      </button>
    </div>
  </section>
</template>