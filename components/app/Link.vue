<script lang="ts">
export default {
  inheritAttrs: false,
}
</script>

<script setup lang="ts">
// eslint-disable-next-line import/first, @typescript-eslint/consistent-type-imports
import type { RouteLocation, RouteLocationRaw } from 'vue-router'
defineProps<{
  to: RouteLocationRaw
  focusTheme?: 'light' | 'dark'
  centered?: boolean
}>()
const localePath = useLocalePath()
</script>

<template>
  <NuxtLink
    v-slot="{ isExactActive, href: slotHref, navigate }"
    :to="localePath(to as unknown as RouteLocation)"
    custom
  >
    <BaseButton
      v-bind="$attrs"
      variant="none"
      size="none"
      :focus-theme="focusTheme"
      :centered="centered"
      :href="slotHref"
      :aria-current="isExactActive ? 'page' : undefined"
      @click="navigate"
    >
      <slot />
    </BaseButton>
  </NuxtLink>
</template>
