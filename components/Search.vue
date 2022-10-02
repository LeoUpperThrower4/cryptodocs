<script setup lang="ts">
  import SearchIcon from './SearchIcon'
  const modifierKey = undefined
</script>

<template>
  <button
  type="button"
  class="group flex h-6 w-6 items-center justify-center sm:justify-start md:h-auto md:w-80 md:flex-none md:rounded-lg md:py-2.5 md:pl-4 md:pr-3.5 md:text-sm md:ring-1 md:ring-slate-200 md:hover:ring-slate-300 dark:md:bg-slate-800/75 dark:md:ring-inset dark:md:ring-white/5 dark:md:hover:bg-slate-700/40 dark:md:hover:ring-slate-500 lg:w-96"
>
 <!-- @click="onOpen" -->
  <SearchIcon class="h-5 w-5 flex-none fill-slate-400 group-hover:fill-slate-500 dark:fill-slate-500 md:group-hover:fill-slate-400" />
  <span class="sr-only md:not-sr-only md:ml-2 md:text-slate-500 md:dark:text-slate-400">
    Search docs
  </span>
    <kbd v-if="modifierKey" class="ml-auto hidden font-medium text-slate-400 dark:text-slate-500 md:block">
      <kbd class="font-sans">{{ modifierKey }}</kbd>
      <kbd class="font-sans">K</kbd>
    </kbd>
</button>
<!-- {isOpen &&
  createPortal(
    <DocSearchModal
      {...docSearchConfig}
      initialScrollY={window.scrollY}
      onClose={onClose}
      hitComponent={Hit}
      navigator={{
        navigate({ itemUrl }) {
          Router.push(itemUrl)
        },
      }}
    />,
    document.body
  )} -->
</template>