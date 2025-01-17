<script setup lang="ts">
import { ref, computed } from 'vue'

const categories = ['All', 'Client', 'App', 'Full Stack']
const selectedCategory = ref('All')

const projects = [
  {
    title: 'Yo-Clicker',
    description: 'A website-app game with awesome features',
    category: 'Full Stack',
    image: 'https://media.discordapp.net/attachments/1326137810415259680/1326138017370607669/Sin_titulo27.png?ex=678b84c5&is=678a3345&hm=0dff39aea64a9c40ca8f840317610110a064560745d75e4397a07dd5aa9cf767&=&format=webp&quality=lossless&width=1193&height=671',
    github: 'https://github.com/YO-CLICKER-TEAM',
    demo: 'https://discord.gg/CM74aYnmz6'
  },
  {
    title: "Dreamin' Things",
    description: 'A Minecraft Forge mod of the videogame Yo-Kai Watch',
    category: 'Client',
    image: 'https://cdn.discordapp.com/attachments/1326143932568178751/1329839525027123220/wallpaper_1.png?ex=678bcd11&is=678a7b91&hm=aa7fa94f4938eeefb55da1b8fb45068a88d6358b37c97efc97f8872ba2838bad&',
    github: 'https://github.com/NullGang/DreaminThingsMod',
    demo: 'https://modrinth.com/mod/dreamin-things-expansion'
  },
  {
    title: 'See U Chat',
    description: 'A webcam social media.',
    category: 'App',
    image: 'https://camo.githubusercontent.com/c3d720b978ec9b2fb36aa912c5ebd364030dc361b254ccc06d81415f444f1570/68747470733a2f2f692e696d6775722e636f6d2f6c3458355a7a6d2e706e67',
    github: 'https://github.com/NullGang/SeeUChat',
    demo: 'https://github.com/NullGang/SeeUChat'
  }
]

const filteredProjects = computed(() => 
  selectedCategory.value === 'All' 
    ? projects 
    : projects.filter(p => p.category === selectedCategory.value)
)
</script>

<template>
  <section id="projects" class="section-padding">
    <div class="max-w-6xl mx-auto">
      <h2 class="text-4xl font-bold mb-12 gradient-text text-center">Projects</h2>
      
      <!-- Category Filter -->
      <div class="flex justify-center gap-4 mb-12">
        <button v-for="category in categories" :key="category"
                @click="selectedCategory = category"
                :class="[
                  'px-4 py-2 rounded-full transition-all duration-300',
                  selectedCategory === category 
                    ? 'bg-gradient-to-r from-primary to-secondary text-white'
                    : 'glass hover:bg-white/20'
                ]">
          {{ category }}
        </button>
      </div>
      
      <!-- Projects Grid -->
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
        <div v-for="project in filteredProjects" :key="project.title"
             class="glass rounded-lg overflow-hidden card-hover group">
          <img :src="project.image" :alt="project.title" class="w-full h-48 object-cover">
          <div class="p-6">
            <h3 class="text-xl font-bold mb-2">{{ project.title }}</h3>
            <p class="text-light/60 mb-4">{{ project.description }}</p>
            <div class="flex gap-4">
              <a :href="project.github" target="_blank" class="btn text-sm">GitHub</a>
              <a :href="project.demo" target="_blank" class="btn text-sm">Live Demo</a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>