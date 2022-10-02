<script setup lang="ts">
  import { ref } from 'vue'
  import GithubIcon from './GithubIcon.vue'
  import MobileNavigation from './MobileNavigation.vue'
  import Logo from './Logo.vue'
  import Logomark from './Logomark.vue'
  import Search from './Search.vue'
  import ThemeSelector from './ThemeSelector.vue'
  
  defineProps({
    navigation: {
      type: Array,
      default: () => []
    }
  })

  const isScrolled = ref(false)
</script>

<template>
  <header
    :class="['sticky top-0 z-50 flex flex-wrap items-center justify-between bg-white px-4 py-5 shadow-md shadow-slate-900/5 transition duration-500 dark:shadow-none sm:px-6 lg:px-8',
      isScrolled
        ? 'dark:bg-slate-900/95 dark:backdrop-blur dark:[@supports(backdrop-filter:blur(0))]:bg-slate-900/75'
        : 'dark:bg-transparent']"
  >
    <div class="mr-6 flex lg:hidden">
      <MobileNavigation :navigation="navigation" />
    </div>
    <div class="relative flex flex-grow basis-0 items-center">
      <NuxtLink :to="'/'" aria-label="Home page">
        <Logomark class="h-9 w-9 lg:hidden" />
        <Logo class="hidden h-9 w-auto fill-slate-700 dark:fill-sky-100 lg:block" />
      </NuxtLink>
    </div>
    <div class="-my-5 mr-6 sm:mr-8 md:mr-0">
      <Search />
    </div>
    <div class="relative flex basis-0 justify-end gap-6 sm:gap-8 md:flex-grow">
      <ThemeSelector class="relative z-10" />
      <NuxtLink :to="'https://github.com/cryptounifier'" target="_blank" class="group" aria-label="GitHub">
        <GithubIcon class="h-6 w-6 fill-slate-400 group-hover:fill-slate-500 dark:group-hover:fill-slate-300" />
      </NuxtLink>
    </div>
  </header>
</template>