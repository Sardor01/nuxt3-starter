<script setup lang="ts">
withDefaults(
  defineProps<{
    is?: 'div' | 'section'
    screen?: 'sm' | 'md' | 'lg' | 'xl' | '2xl' | ''
  }>(), {
    is: 'div',
  },
)
</script>

<template>
  <component :is="is" class="!w-full mx-auto px-4" :class="screen ? `${screen}container` : 'sm:container'">
    <slot />
  </component>
</template>
