<script setup lang="ts">
import type { SelectTriggerProps } from 'reka-ui'
import type { HTMLAttributes } from 'vue'
import { ChevronDown } from 'lucide-vue-next'
import { SelectIcon, SelectTrigger, useForwardProps } from 'reka-ui'
import { computed } from 'vue'
import { cn } from '../../../lib/utils'

const props = defineProps<SelectTriggerProps & { class?: HTMLAttributes['class'] }>()

const delegatedProps = computed(() => {
  const { class: _, ...delegated } = props

  return delegated
})

const forwardedProps = useForwardProps(delegatedProps)
</script>

<template>
  <SelectTrigger
    v-bind="forwardedProps"
    :class="cn(
      'flex h-10 w-full items-center justify-between rounded-md border border-input bg-muted px-3 py-2 text-sm ring-offset-background placeholder:text-muted-foreground focus:outline-none focus:ring-2 focus:ring-ring focus:ring-offset-2 disabled:cursor-not-allowed disabled:opacity-50 [&>span]:line-clamp-1',
      props.class,
    )"
  >
    <slot />
    <SelectIcon as-child>
      <ChevronDown class="w-4 h-4 opacity-50" />
    </SelectIcon>
  </SelectTrigger>
</template>
