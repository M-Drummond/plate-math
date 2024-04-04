<script setup lang="ts">
import { ref } from 'vue'

import HeaderBar from '@/components/HeaderBar.vue'
import TotalWeight from '@/components/TotalWeight.vue'
import FooterBar from '@/components/FooterBar.vue'
</script>

<script lang="ts">
interface Plate {
  label: string
  weight: number
  count: number
  color: string
}

export const barWeight = ref<number>(20)

export const loadedPlates = ref<Record<string, Plate>>({
  twenties: {
    label: '20kgs',
    weight: 20,
    count: 0,
    color: 'blue'
  },
  tens: {
    label: '10kgs',
    weight: 10,
    count: 0,
    color: 'green'
  },
  fives: {
    label: '5kgs',
    weight: 5,
    count: 0,
    color: 'gray'
  },
  'two-fives': {
    label: '2.5kgs',
    weight: 2.5,
    count: 0,
    color: 'pink'
  }
})

export var leftyMode = ref(true)

export function toggleHandMode() {
  leftyMode.value = !leftyMode.value
}

export function reset() {
  for (const plate in loadedPlates.value) {
    loadedPlates.value[plate].count = 0
  }
}
</script>

<template>
  <main class="flex flex-col font-bold text-center p-0 min-h-[90vmax] overflow-x-hidden">
    <HeaderBar />

    <div
      class="relative flex items-center px-4 mb-4 space-x-1"
      :class="leftyMode ? 'justify-end ml-12  ' : ''"
      v-for="(plate, plateKey) in loadedPlates"
      :key="plateKey"
    >
      <button
        @click="loadedPlates[plateKey].count++"
        v-if="loadedPlates[plateKey]"
        :class="[leftyMode ? 'order-last' : '', `bg-${loadedPlates[plateKey].color}-200`]"
        class="p-2 left-0 dark:bg-opacity-0 w-[50px] h-[50px] flex flex-col items-center justify-center number transition-all aspect-square relative z-[9999] border-solid border text-xl"
        id="20kg+"
      >
        {{ loadedPlates[plateKey].weight }}
      </button>

      <transition-group :name="leftyMode ? 'move-left' : 'move-right'">
        <button
          @click="loadedPlates[plateKey].count--"
          v-for="index in loadedPlates[plateKey].count"
          :key="index"
          :class="`bg-${loadedPlates[plateKey].color}-800`"
          class="p-2 w-[50px] h-[50px] bg-opacity-20 dark:bg-opacity-0 border-4 flex flex-col items-center justify-center number aspect-square relative z-0 rounded-full border-solid text-xl"
        >
          {{ loadedPlates[plateKey].weight }}
        </button>
      </transition-group>
    </div>

    <TotalWeight />

    <FooterBar />
  </main>
</template>
