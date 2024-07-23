<script setup lang="ts">
import { Icon } from '@iconify/vue'
import { Button } from '@/components/ui/button'
import { Separator } from '@/components/ui/separator'

const colorMode = useColorMode()

function changeColorMode(): void {
  if (colorMode.value === 'dark') {
    colorMode.preference = 'light';
    return;
  }

  colorMode.preference = 'dark';
}

function logoPath(): string {
  if (colorMode.value === 'dark') {
    return '/images/logo-white.svg';
  }

  return '/images/logo.svg';
}
</script>

<template>
  <Button variant="outline" @click="changeColorMode" class="absolute top-4 right-4">
    <Icon icon="radix-icons:moon" class="h-[1.2rem] w-[1.2rem] rotate-0 scale-100 transition-all dark:-rotate-90 dark:scale-0" />
    <Icon icon="radix-icons:sun" class="absolute h-[1.2rem] w-[1.2rem] rotate-90 scale-0 transition-all dark:rotate-0 dark:scale-100" />
    <span class="sr-only">Toggle theme</span>
  </Button>

  <div class="flex mt-8">
    <NuxtImg class="mx-auto" :src="logoPath()" placeholder width="200" />
  </div>

  <div class="container my-8">
    <NuxtPage />
  </div>
</template>
