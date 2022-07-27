<template>
  <pre>
    <code :class="'language-' + codeLanguage">
      {{ code }}
    </code>
  </pre>
</template>

<script>
import 'prismjs'
import 'prismjs/themes/prism.css'

const defaultCodeLanguage = 'javascript'
const defaultCode = `export default {
      strategy: 'predictive', 
      engine: {
        cpus: 12,
        backups: ['./storage/cache.wtf'],
    },
  }`

export default {
  props: {
    codeLanguage: { type: String, default: defaultCodeLanguage },
    code: { type: String, default: defaultCode }
  }
}
</script>
