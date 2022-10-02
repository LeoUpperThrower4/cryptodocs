<script setup lang="ts">
  import { ref } from 'vue'
  import {
    Listbox,
    ListboxButton,
    ListboxOptions,
    ListboxLabel,
    ListboxOption,
  } from '@headlessui/vue'
  
  import LightIcon from './LightIcon.vue'
  import DarkIcon from './DarkIcon.vue'
  import SystemIcon from './SystemIcon.vue'
  
  const themes = [
    { name: 'Light', value: 'light', icon: LightIcon },
    { name: 'Dark', value: 'dark', icon: DarkIcon },
    { name: 'System', value: 'system', icon: SystemIcon },
  ]
  
  const selectedTheme = ref(themes[0])
  
  watch(selectedTheme, () => {
    document.documentElement.setAttribute('theme', selectedTheme.value.value)
    document.documentElement.setAttribute('data-theme', selectedTheme.value.value)
    localStorage.setItem('theme', selectedTheme.value.value)
  })
  
  function listboxOptionClass(theme) {
    return ['flex cursor-pointer select-none items-center rounded-[0.625rem] p-1',
                {
                  'text-sky-500': theme.selected,
                  'text-slate-900 dark:text-white': theme.active && !theme.selected,
                  'text-slate-700 dark:text-slate-400': !theme.active && !theme.selected,
                  'bg-slate-100 dark:bg-slate-900/40': theme.active,
                }]
  }
  
  function themeIconClass(selected) {
    return `h-4 w-4' ${selected ? 'fill-sky-400 dark:fill-sky-400' : 'fill-slate-400'}`
  }
</script>

<template>
    <Listbox
      as="div"
      v-model="selectedTheme"
    >
      <ListboxLabel class="sr-only">Theme</ListboxLabel>
      <ListboxButton
        class="flex h-6 w-6 items-center justify-center rounded-lg shadow-md shadow-black/5 ring-1 ring-black/5 dark:bg-slate-700 dark:ring-inset dark:ring-white/5"
        :aria-label="selectedTheme?.name"
      >
        <LightIcon class="hidden h-4 w-4 fill-sky-400 [[data-theme=light]_&]:block" />
        <DarkIcon class="hidden h-4 w-4 fill-sky-400 [[data-theme=dark]_&]:block" />
        <LightIcon class="hidden h-4 w-4 fill-slate-400 [:not(.dark)[data-theme=system]_&]:block" />
        <DarkIcon class="hidden h-4 w-4 fill-slate-400 [.dark[data-theme=system]_&]:block" />
      </ListboxButton>
      <ListboxOptions class="absolute top-full left-1/2 mt-3 w-36 -translate-x-1/2 space-y-1 rounded-xl bg-white p-3 text-sm font-medium shadow-md shadow-black/5 ring-1 ring-black/5 dark:bg-slate-800 dark:ring-white/5">
        <ListboxOption v-for="theme in themes" :key="theme.name" :value="theme" :class="listboxOptionClass(theme)" v-slot="{ selected }">
          <div class="rounded-md bg-white p-1 shadow ring-1 ring-slate-900/5 dark:bg-slate-700 dark:ring-inset dark:ring-white/5">
            <component 
              :is="theme.icon"
              :class="themeIconClass(selected)"
            />
          </div>
          <div class="ml-3">{{theme.name}}</div>
        </ListboxOption>
      </ListboxOptions>
    </Listbox>
</template>