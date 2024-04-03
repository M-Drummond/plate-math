<script setup lang="ts">
import { ref, computed } from 'vue';

const barWeight = ref<number>(20)

interface Plate {
  label: string
  weight: number
  count: number
  color: string
}

const loadedPlates = ref<Record<string, Plate>>({
  twenties: {
    label: "20kgs",
    weight: 20,
    count: 0,
    color: "blue"
  },
  tens: {
    label: "10kgs",
    weight: 10,
    count: 0,
    color: "green"
  },
  fives: {
    label: "5kgs",
    weight: 5,
    count: 0,
    color: "gray"
  },
  "two-fives": {
    label: "2.5kgs",
    weight: 2.5,
    count: 0,
    color: "pink"
  }
});

const computedTotal = computed<number>(() => {
  let total = 0;
  for (const plate in loadedPlates.value) {
    total += loadedPlates.value[plate].count * loadedPlates.value[plate].weight;
  }
  total += barWeight.value
  return total;
});

function reset() {
  for (const plate in loadedPlates.value) {
    loadedPlates.value[plate].count = 0
  }
}

var leftyMode = ref(true)

function toggleHandMode() {
  leftyMode.value = !leftyMode.value;
  console.log(leftyMode)
}

</script>

<template>
  <main class=" flex flex-col font-bold text-center p-0 min-h-[90vmax]   overflow-x-hidden">

    <div
      class="flex flex-row items-center justify-between p-2 mb-8 font-bold border-b-8 border-current dark:border-teal-700 dark:bg-orange-400 dark:text-slate-800">
      <button class="p-2 transition-opacity border border-current border-solid number "
        :class="barWeight == 20 ? '' : 'opacity-25'" @click="barWeight = 20">
        20
      </button>
      <span>Plate Math</span>
      <button class="p-2 transition-opacity border border-black border-solid number dark:border-white"
        :class="barWeight == 15 ? '' : 'opacity-25'" @click="barWeight = 15">
        15
      </button>
    </div>

    <!--  -->

    <div class="relative flex items-center px-4 mb-4 space-x-1" :class="leftyMode ? 'justify-end ml-12  ' : ''"
      v-for="(plate, plateKey) in loadedPlates" :key="plateKey">
      <button @click="loadedPlates[plateKey].count++" v-if="loadedPlates[plateKey]"
        :class="[leftyMode ? 'order-last' : '', `bg-${loadedPlates[plateKey].color}-200`]"
        class="p-2 left-0 dark:bg-opacity-0 w-[50px] h-[50px] flex flex-col items-center justify-center number  transition-all aspect-square relative z-[9999] border-solid border text-xl  "
        id="20kg+"> {{
          loadedPlates[plateKey].weight }}</button>

      <transition-group :name="leftyMode ? 'move-left' : 'move-right'">

        <button @click="loadedPlates[plateKey].count--" v-for="index in loadedPlates[plateKey].count" :key="index"
          :class="`bg-${loadedPlates[plateKey].color}-800`"
          class="p-2 w-[50px] h-[50px] bg-opacity-20 dark:bg-opacity-0 border-4 flex flex-col items-center justify-center number aspect-square relative z-0   rounded-full  border-solid border  text-xl">
          {{
          loadedPlates[plateKey].weight }}</button>

      </transition-group>
    </div>

    <!-- dark:text-orange-400 dark:bg-slate-800 -->

    <div :class="leftyMode ? 'before:skew-x-12' : 'before:skew-x-[-12deg]'"
      class="relative pt-5 mt-8 transition-all dark:text-slate-800 before:w-2/3 before:mx-auto before:h-full before:z-0 before:inset-0 before:bg-gray-300 before:dark:bg-orange-400 before:absolute">
      <p class="mb-8 text-[50px] dark:text-teal-700 font-[900] number relative z-20 py-4">{{ computedTotal }}</p>

      <span class="absolute left-0 right-0 text-2xl font-bold dark:text-teal-700 bottom-6">Total KG</span>

    </div>
    <div
      class="fixed bottom-0 flex flex-row items-center justify-between w-full p-4 mt-8 border-t-8 border-current dark:border-teal-700 ">

      <button class="p-2 border border-black border-solid focus:border-double active:border-double dark:border-white"
        @click="reset">
        Reset All
      </button>
      <button @click="toggleHandMode"
        class="p-2 border border-black border-solid focus:border-double active:border-double dark:border-white"
        v-text="leftyMode ? 'Left Handed' : 'Right Handed'"></button>
    </div>

  </main>
</template>
