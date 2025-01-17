<script setup lang="ts">
import { ref } from 'vue'

const skills = [
  { name: 'HTML5', icon: '🌐' },
  { name: 'CSS3', icon: '🎨' },
  { name: 'JavaScript', icon: '⚡' },
  { name: 'Vue.js', icon: '💚' },
  { name: 'React', icon: '⚛️' },
  { name: 'Node.js', icon: '🚀' },
  { name: 'TypeScript', icon: '📘' },
  { name: 'FL Studio', icon: '🍓' }
]

const milestones = [
  {
    year: '2024',
    title: 'Full Developer',
    description: 'Leading development teams and architecting solutions'
  },
  {
    year: '2022',
    title: 'Full Stack Developer',
    description: 'Building end-to-end applications'
  },
  {
    year: '2020',
    title: 'Frontend Developer',
    description: 'Specializing in modern web frameworks'
  },
  {
    year: '2018',
    title: 'Started Coding Journey',
    description: 'First line of code written'
  }
]
</script>

<template>
  <section id="about" class="section-padding bg-dark/50">
    <div class="max-w-6xl mx-auto">
      <h2 class="text-4xl font-bold mb-12 gradient-text text-center">About Me</h2>
      
      <!-- Skills -->
      <div class="grid grid-cols-2 md:grid-cols-4 gap-6 mb-16">
        <div v-for="skill in skills" :key="skill.name"
             class="glass p-6 rounded-lg text-center card-hover">
          <div class="text-4xl mb-2">{{ skill.icon }}</div>
          <div class="font-medium">{{ skill.name }}</div>
        </div>
      </div>
      
      <!-- Timeline -->
      <div class="space-y-8">
        <div v-for="milestone in milestones" :key="milestone.year"
             class="glass p-6 rounded-lg card-hover">
          <div class="flex items-center gap-4">
            <div class="text-2xl font-bold gradient-text">{{ milestone.year }}</div>
            <div>
              <h3 class="text-xl font-semibold">{{ milestone.title }}</h3>
              <p class="text-light/60">{{ milestone.description }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>