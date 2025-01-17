<script setup lang="ts">
import { ref, onMounted } from 'vue'
import loader from '@monaco-editor/loader'

const editorContainer = ref<HTMLElement | null>(null)
const editor = ref(null)
const output = ref('')
const isDarkMode = ref(true)

const defaultCode = `function greet(name) {
  return \`Hello, \${name}!\`;
}

console.log(greet('World'));`

onMounted(async () => {
  if (editorContainer.value) {
    loader.init().then(monaco => {
      editor.value = monaco.editor.create(editorContainer.value!, {
        value: defaultCode,
        language: 'javascript',
        theme: isDarkMode.value ? 'vs-dark' : 'vs',
        minimap: { enabled: false },
        fontSize: 14,
        automaticLayout: true
      })
    })
  }
})

const toggleTheme = () => {
  isDarkMode.value = !isDarkMode.value
  if (editor.value) {
    editor.value.updateOptions({
      theme: isDarkMode.value ? 'vs-dark' : 'vs'
    })
  }
}

const runCode = () => {
  try {
    const code = editor.value?.getValue()
    const result = eval(code)
    output.value = String(result)
  } catch (error) {
    output.value = `Error: ${error.message}`
  }
}
</script>

<template>
  <section id="code-editor" class="section-padding">
    <div class="max-w-6xl mx-auto">
      <h2 class="text-4xl font-bold mb-12 gradient-text text-center">Try Some Code</h2>
      
      <div class="glass p-6 rounded-lg">
        <div class="flex justify-end gap-4 mb-4">
          <button @click="toggleTheme" class="btn text-sm">
            {{ isDarkMode ? '☀️ Light' : '🌙 Dark' }}
          </button>
          <button @click="runCode" class="btn text-sm">▶️ Run Code</button>
        </div>
        
        <div ref="editorContainer" class="h-[400px] mb-4 rounded-lg overflow-hidden"></div>
        
        <div class="glass p-4 rounded-lg">
          <h3 class="text-lg font-semibold mb-2">Output:</h3>
          <pre class="font-mono text-sm">{{ output }}</pre>
        </div>
      </div>
    </div>
  </section>
</template>