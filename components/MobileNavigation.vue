<script setup lang="ts">
  import MenuIcon from './MenuIcon.vue'
  import CloseIcon from './CloseIcon.vue'
  import { ref } from 'vue'
  import {
    Dialog,
    DialogPanel,
    DialogTitle,
    DialogDescription,
  } from '@headlessui/vue'

  defineProps({
    navigation: {
      type: Array,
      default: () => []
    }
  })
  const isOpen = ref(true)

  function setIsOpen(value) {
    isOpen.value = value
  }
  
</script>

<template>
  <button
    type="button"
    @click="setIsOpen(true)"
    class="relative"
    aria-label="Open navigation"
  >
    <MenuIcon class="h-6 w-6 stroke-slate-500" />
  </button>
  <Dialog
    :open="isOpen" 
    @close="setIsOpen"
    class="fixed inset-0 z-50 flex items-start overflow-y-auto bg-slate-900/50 pr-10 backdrop-blur lg:hidden"
    aria-label="Navigation"
  >
    <DialogPanel class="min-h-full w-full max-w-xs bg-white px-4 pt-5 pb-12 dark:bg-slate-900 sm:px-6">
      <div class="flex items-center">
        <button
          type="button"
          @click="setIsOpen(false)"
        >
          <CloseIcon class="h-6 w-6 stroke-slate-500" />
        </button>
        <NuxtLink :to="'/'" class="ml-6" aria-label="Home page">
          <Logomark class="h-9 w-9" />
        </NuxtLink>
      </div>
      <Navigation :navigation='navigation' class="mt-5 px-1" />
    </DialogPanel>
  </Dialog>
</template>