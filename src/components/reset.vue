<template>
    <div class="flex flex-row items-center mb-8 mt-auto justify-center">
        <button class="border border-solid focus:border-double active:border-double border-black  dark:border-white p-2"
            @click="resetWeight">
            Reset All
        </button>
    </div>
</template>


<script setup lang="ts">

import { loadedPlates } from '../views/HomeView.vue'


</script>

<script lang="ts">
export function resetWeight() {
    for (const plate in loadedPlates.value) {
        loadedPlates.value[plate].count = 0
    }
}

</script>