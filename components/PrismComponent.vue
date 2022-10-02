<script setup lang="ts">
  import 'prismjs'
  import 'prismjs/themes/prism.css'
  
  defineProps({
    code: {
      type: String,
      default: `export default {
        strategy: 'predictive', 
        engine: {
          cpus: 12,
          backups: ['./storage/cache.wtf'],
      },
    }`
    },
    codeLanguage: {
      type: String,
      default: 'javascript'
    }
  })
</script>
  
<template>
  <pre>
    <code :class="'language-' + codeLanguage">
      {{ code }}
    </code>
  </pre>
</template>