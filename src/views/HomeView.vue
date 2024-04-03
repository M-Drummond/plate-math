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
  <main class=" flex flex-col da  text-center p-4  min-h-[90vmax] my-1 mx-1 overflow-x-hidden">

    <div class="flex flex-row items-center mb-8 border-b pb-4 border-solid  justify-between">
      <button class="border border-solid number transition-opacity border-black dark:border-white p-2"
        :class="barWeight == 20 ? '' : 'opacity-25'" @click="barWeight = 20">
        20
      </button>
      <span>Bar Weight</span>
      <button class="border border-solid number transition-opacity border-black dark:border-white p-2"
        :class="barWeight == 15 ? '' : 'opacity-25'" @click="barWeight = 15">
        15
      </button>
    </div>

    <!--  -->

    <div class="flex    space-x-1 items-center  relative mb-4" :class="leftyMode ? 'justify-end ml-12  ' : ''"
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
      class=" dark:text-slate-800 mt-8 pt-5 transition-all relative before:w-2/3 before:mx-auto before:h-full before:z-0 before:inset-0 before:dark:bg-orange-400 before:absolute ">
      <p class="mb-8 text-[50px]  font-[900] number relative z-20 py-4">{{ computedTotal }}</p>

      <span class="absolute bottom-6 left-0 right-0 text-2xl font-bold">Total</span>

    </div>
    <div class="flex flex-row items-center mb-8 mt-auto justify-between">

      <button class="border border-solid focus:border-double active:border-double border-black  dark:border-white p-2"
        @click="reset">
        Reset All
      </button>
      <button @click="toggleHandMode"
        class="border border-solid focus:border-double active:border-double border-black  dark:border-white p-2"
        v-text="leftyMode ? 'Left Handed' : 'Right Handed'"></button>
    </div>

  </main>
</template>
