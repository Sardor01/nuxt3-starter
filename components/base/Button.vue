<script setup lang="ts">
const props = withDefaults(
  defineProps<{
    type?: 'button' | 'submit'
    variant?: 'blue' | 'red' | 'gray' | 'blue-red' | 'none'
    size?: 'sm' | 'md' | 'lg' | 'link' | 'none'
    focusTheme?: 'light' | 'dark'
    href?: string
    link?: boolean
    loading?: boolean
    disabled?: boolean
    centered?: boolean
    active?: boolean
    exactActive?: boolean
  }>(), {
    type: 'button',
    variant: 'blue',
    size: 'md',
    focusTheme: 'dark',
    centered: true,
  },
)

const disableButton = computed(() => {
  return props.disabled || props.loading
})

const btnVariant = computed(() => {
  switch (props.variant) {
    case 'red': {
      if (props.link)
        return 'text-red focus-visible:ring-red/30'
      return 'bg-red text-white border border-red hover:bg-red-light hover:border-red-light focus-visible:ring-red/30'
    }
    case 'blue': {
      if (props.link)
        return 'text-blue focus-visible:ring-blue/30'
      return 'bg-blue text-white border border-blue hover:bg-blue-light hover:border-blue-light focus-visible:ring-blue/30'
    }
    default:
      return props.focusTheme === 'dark' ? 'focus-visible:ring-blue/30' : 'focus-visible:ring-gray-light/50'
  }
})

const btnSize = computed(() => {
  switch (props.size) {
    case 'sm': {
      return {
        base: 'min-w-[120px] h-11 text-sm rounded-2xl px-3 py-2',
        icon: 'fa-xl',
      }
    }
    case 'md': {
      return {
        base: 'min-w-[120px] h-12 text-base rounded-2xl px-4 py-3',
        icon: 'fa-xl',
      }
    }
    case 'lg': {
      return {
        base: 'min-w-[120px] h-13 text-lg rounded-2xl px-6 py-4',
        icon: 'fa-xl',
      }
    }
    case 'link': {
      return {
        base: 'text-base rounded-lg p-1',
        icon: 'fa-xl',
      }
    }
    default: {
      return { base: '', icon: '' }
    }
  }
})
</script>

<template>
  <component
    :is="href ? 'a' : 'button'"
    :href="href"
    :type="href ? undefined : type"
    class="inline-flex items-center transition-colors ease-in-out duration-150 font-semibold whitespace-nowrap select-none focus:outline-none focus-visible:ring"
    :class="[
      btnVariant,
      btnSize.base,
      centered && 'justify-center text-center',
      disableButton && 'pointer-events-none opacity-80',
    ]"
  >
    <FontAwesomeIcon
      v-if="loading"
      icon="fa-solid fa-spinner"
      class="fa-spin"
      :class="btnSize.icon"
    />
    <slot v-else />
  </component>
</template>
