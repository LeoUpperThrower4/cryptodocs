<template>
  <NuxtPage />
</template>
<script setup>
onMounted(() => {
  const theme = localStorage.getItem('theme') || 'system'
  document.documentElement.setAttribute('theme', theme)
  document.documentElement.setAttribute('data-theme', theme)
})
</script>