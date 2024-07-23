<script setup lang="ts">
import { type HTMLAttributes, computed } from 'vue'
import { cn } from '@/lib/utils'

const props = defineProps<
    { class?: HTMLAttributes['class'], label?: string }
>()

const delegatedProps = computed(() => {
  const { class: _, ...delegated } = props

  return delegated
})
</script>

<template>
  <div
    v-bind="delegatedProps"
    :class="
      cn(
          'border-b border-gray-200 pb-2',
          props.class,
      )
    "
  >
    <h3
      v-if="props.label"
      :class="cn('text-base font-semibold leading-6')"
    >{{ props.label }}</h3>
  </div>
</template>
