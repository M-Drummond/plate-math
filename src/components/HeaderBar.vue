<template>
    <div
        class="flex flex-row items-center justify-between p-2 mb-8 font-bold border-b-8 border-current dark:border-teal-700 dark:bg-orange-400 dark:text-slate-800">
        <div class="flex flex-row space-x-2">
            <button class="p-2 transition-opacity border border-current border-solid number dark:border-white "
                :class="barWeight == 0 ? '' : 'opacity-25'" @click="barWeight = 0">
                0
            </button>
            <button class="p-2 transition-opacity border border-black border-solid number dark:border-white"
                :class="barWeight == 15 ? '' : 'opacity-25'" @click="barWeight = 15">
                15
            </button>
            <button class="p-2 transition-opacity border border-current border-solid number dark:border-white"
                :class="barWeight == 20 ? '' : 'opacity-25'" @click="barWeight = 20">
                20
            </button>

        </div>
        <span>Plate Math</span>

    </div>
</template>

<script lang="ts">

</script>

<script setup lang="ts">

import { barWeight } from '@/views/HomeView.vue';

</script>

<style scoped></style>
