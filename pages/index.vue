<script setup lang="ts">
import { onMounted } from 'vue'
import { useStorage } from '@vueuse/core'
import { Checkbox } from '@/components/ui/checkbox'
import { Heading } from '@/components/ui/heading'
import { Skeleton } from '@/components/ui/skeleton'

let loading = ref(true);

const { status, data: categories } = await useFetch('http://localhost:8000/api/festival-list', {
  server: false,
  lazy: true
});

const data = [{
  name: 'Geld & Finanzen',
  items: [{id: 1, value: 1}, {id: 2, value: 2}],
}, {
  name: 'Hygiene',
  items: [{id: 3, value: 'Deo (Reisegröße)'}, {id: 4, value: 'Reiseset: Shampoo, Spülung etc.'}],
}, {
  name: 'Kleidung',
  items: [{id: 5, value: 'Badesachen'}, {id: 6, value: 'Fleecepullover/-jacke'}],
}];

const checked = useStorage('checked', [])

function handleChange(id: number): void {
  if (checked.value.includes(id)) {
    checked.value.splice(checked.value.indexOf(id), 1);
    return;
  }

  checked.value.push(id);
}

onMounted(async () => {
  loading.value = false;
})
</script>

<template>
  <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-16">
    <div v-for="category in categories" v-if="!loading && status !== 'pending'">
      <Heading :label="category.name" />

      <div v-for="item in category.items">
        <div class="items-top flex items-center gap-x-2 mt-2">
          <Checkbox :id="`item-${item.id}`" :checked="checked.includes(item.id)" @update:checked="handleChange(item.id)" />
          <div class="grid gap-1.5 leading-none">
            <label
                :for="`item-${item.id}`"
                class="text-sm font-medium leading-none peer-disabled:cursor-not-allowed peer-disabled:opacity-70"
            >
              {{ item.name }}
            </label>
          </div>
        </div>
      </div>
    </div>

    <template v-else>
      <div class="flex items-center space-x-4">
        <Skeleton class="h-12 w-12 rounded-full" />
        <div class="space-y-2">
          <Skeleton class="h-4 w-[250px]" />
          <Skeleton class="h-4 w-[200px]" />
        </div>
      </div>

      <div class="flex items-center space-x-4">
        <Skeleton class="h-12 w-12 rounded-full" />
        <div class="space-y-2">
          <Skeleton class="h-4 w-[250px]" />
          <Skeleton class="h-4 w-[200px]" />
        </div>
      </div>

      <div class="flex items-center space-x-4">
        <Skeleton class="h-12 w-12 rounded-full" />
        <div class="space-y-2">
          <Skeleton class="h-4 w-[250px]" />
          <Skeleton class="h-4 w-[200px]" />
        </div>
      </div>
    </template>
  </div>
</template>
