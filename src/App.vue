<script setup lang="ts">
import { onMounted, ref } from 'vue'
import { useMotion } from '@vueuse/motion'
import HeroSection from './components/HeroSection.vue'
import AboutSection from './components/AboutSection.vue'
import ProjectsSection from './components/ProjectsSection.vue'
//import CodeEditorSection from './components/CodeEditorSection.vue'
import ContactSection from './components/ContactSection.vue'
import FooterSection from './components/FooterSection.vue'

//@ts-ignore
const { isSupported } = useMotion()
const cursor = ref({ x: 0, y: 0 })
const cursorVisible = ref(false)

onMounted(() => {
  if (!isSupported) {
    console.warn('Motion is not supported on this device')
  }

  // Custom cursor
  let cursorTimeout: number
  
  window.addEventListener('mousemove', (e) => {
    cursorVisible.value = true
    clearTimeout(cursorTimeout)
    
    // Hide cursor when not moving
    //@ts-ignore
    cursorTimeout = setTimeout(() => {
      cursorVisible.value = false
    }, 3000)

    // Smooth cursor movement using requestAnimationFrame
    const updateCursor = () => {
      const dx = e.clientX - cursor.value.x
      const dy = e.clientY - cursor.value.y
      
      cursor.value = {
        x: cursor.value.x + dx * 0.2,
        y: cursor.value.y + dy * 0.2
      }

      if (Math.abs(dx) > 0.1 || Math.abs(dy) > 0.1) {
        requestAnimationFrame(updateCursor)
      }
    }
    
    requestAnimationFrame(updateCursor)
  })

  // Hide cursor when leaving window
  window.addEventListener('mouseout', () => {
    cursorVisible.value = false
  })

  // Show cursor when entering window
  window.addEventListener('mouseover', () => {
    cursorVisible.value = true
  })
})
</script>

<template>
  <main class="min-h-screen bg-dark">
    <!-- Custom cursor -->
    <div
      class="custom-cursor"
      :class="{ 'cursor-visible': cursorVisible }"
      :style="{
        left: cursor.x + 'px',
        top: cursor.y + 'px'
      }"
    ></div>

    <HeroSection />
    <AboutSection />
    <ProjectsSection />
    <!--<CodeEditorSection />-->
    <ContactSection />
    <FooterSection />
  </main>
</template>