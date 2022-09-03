<script setup>

import { useDark, useToggle } from '@vueuse/core'

const isDark = useDark()

const toggleDark = useToggle(isDark)

</script>

<template>
    <button @click="toggleDark()">
        <div class="flex flex-row items-center mt-3 md:mt-8">
            <div class="font-bold text-xl mr-3">
                Dark Mode
            </div>
            <!-- Slider -->
            <div class="bg-zinc-800 dark:bg-zinc-100 transition ease-in-out
            duration-200 rounded-full px-5 py-0">
                <div class="bg-zinc-100 dark:bg-zinc-800 border-4
                border-zinc-800 dark:border-zinc-100 rounded-full 
                -translate-x-5 dark:translate-x-5 transition ease-in-out
                duration-200 p-3"></div>
            </div>
        </div>
    </button>
</template>