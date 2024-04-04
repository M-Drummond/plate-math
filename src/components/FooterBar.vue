<template>
  <div
    class="fixed bottom-0 flex flex-row items-center justify-between w-full p-4 mt-8 border-t-8 border-current dark:border-teal-700"
  >
    <button
      class="p-2 border border-black border-solid focus:border-double active:border-double dark:border-white"
      @click="reset"
    >
      Reset All
    </button>
    <button
      @click="toggleHandMode"
      class="p-2 border border-black border-solid focus:border-double active:border-double dark:border-white"
      v-text="leftyMode ? 'Left Handed' : 'Right Handed'"
    ></button>
  </div>
</template>

<script lang="ts"></script>

<script setup lang="ts">
import { leftyMode, toggleHandMode, reset } from '@/views/HomeView.vue'
</script>

<style scoped></style>
