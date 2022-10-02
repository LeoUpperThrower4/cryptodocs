<script setup lang="ts">
  const styles = {
    primary:
      'rounded-full bg-sky-300 py-2 px-4 text-sm font-semibold text-slate-900 hover:bg-sky-200 focus:outline-none focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-sky-300/50 active:bg-sky-500',
    secondary:
      'rounded-full bg-slate-800 py-2 px-4 text-sm font-medium text-white hover:bg-slate-700 focus:outline-none focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-white/50 active:text-slate-400'
  }
  const props = defineProps({
    variant: {
      type: String,
      default: 'primary'
    },
    className: {
      type: String,
      default: ''
    }
  })
  function finalClassName () {
    return [styles[props.variant], props.className]
  }
</script>

<template>
  <a v-bind="$attrs" :class="finalClassName()">
    <slot />
  </a>
</template>