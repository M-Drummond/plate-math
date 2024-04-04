<template>
  <div
    class="relative pt-5 mt-8 transition-all dark:text-slate-800 before:w-2/3 before:mx-auto before:h-full before:z-0 before:inset-0 before:bg-gray-300 before:dark:bg-orange-400 before:absolute"
  >
    <p class="mb-8 text-[50px] dark:text-teal-700 font-[900] number relative z-20 py-4">
      {{ computedTotal }}
    </p>
    <span class="absolute left-0 right-0 text-2xl font-bold dark:text-teal-700 bottom-6"
      >Total KG</span
    >
  </div>
</template>

<script setup lang="ts">
import { computed } from 'vue'

import { loadedPlates, barWeight } from '@/views/HomeView.vue'

const computedTotal = computed<number>(() => {
  let total = 0
  for (const plate in loadedPlates.value) {
    total += loadedPlates.value[plate].count * loadedPlates.value[plate].weight
  }
  total += barWeight.value
  return total
})
</script>

<style scoped></style>
