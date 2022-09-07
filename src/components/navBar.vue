<script setup>
import { ref } from "@vue/reactivity"
import { computed } from "@vue/runtime-core"
import darkMode from "./darkMode.vue"

const props = defineProps({
    linkMsg: String,
    linkHref: String
})


// opacity of social media icons
const ghSelect = ref(0)

let ghCss = 'opacity-100'
let ytCss = 'opacity-100'

const ghOpacity = computed(() => {
    switch (ghSelect.value) {
        case (0):
            ghCss = 'opacity-100'
            ytCss = 'opacity-100'
            break

        case (1):
            ghCss = 'opacity-100'
            ytCss = 'opacity-75'
            break

        case (2):
            ghCss = 'opacity-75'
            ytCss = 'opacity-100'
            break
    }
    return { ghCss, ytCss }
})
    

</script>

<template>
    <!-- Dark Mode button (for mobile) -->
    <div class="flex justify-between items-center md:hidden pt-3 px-3 md:pt-0 md:px-0">
        <darkMode /> 
        <div class="font-bold dark:text-zinc-900  bg-zinc-300 
        hover:bg-zinc-400 rounded-lg
        transition ease-in-out duration-300 p-1 px-3 mt-3">
            <router-link :to="linkHref">{{ linkMsg }}</router-link>
        </div>
    </div>

    <div class="flex flex-col md:flex-row justify-center md:justify-between items-center mx-10 md:mx-32 pt-8 md:pt-10">
        <!-- Title & description -->
        <div>
            <div class="mb-3 md:mb-0">
                <span class="font-mono font-bold text-5xl md:text-2xl">
                    ./Benkyou
                </span>
            </div>

            <span class="text-sm hidden md:flex">
                Simple Pomodoro timer & todo-list app | 
                Tristan Shawn den Ouden 2022
            </span>

            <!-- Dark Mode button (for PC) -->
            <div class="hidden md:flex">
                <darkMode />
            </div>
        </div>
        <!-- Description for Mobile -->
        <div class="text-center font-mono text-sm md:hidden mb-3">
            Simple Pomodoro timer & todo-list<br> By Tristan Shawn den Ouden
            
        </div>
        <!-- Social media links -->
        <div class="flex flex-row items-center select-none">
            <!-- Github icons -->
            <a href="https://github.com/tsdenouden" target="_blank" 
            rel="noopener noreferrer" @mouseover="ghSelect = 1" @mouseleave="ghSelect = 0" 
            class="mr-3">
                <!-- Github dark icon -->
                <img src="../assets/images/github-icon-light.png" alt="Github icon"
                class="hidden dark:flex md:hover:-translate-y-1 transition ease-in-out" 
                :class="ghOpacity.ghCss" draggable="false">
                <!-- Github light icon -->
                <img src="../assets/images/github-icon-dark.png" alt="Github icon"
                class="flex dark:hidden md:hover:-translate-y-1 transition ease-in-out" 
                :class="ghOpacity.ghCss" draggable="false">
            </a>
            <!-- Youtube Icons -->
            <a href="https://www.youtube.com/channel/UCFtJ-g7eYrA9LUcaSOiBBBA" target="_blank" 
            rel="noopener noreferrer" @mouseover="ghSelect = 2" @mouseleave="ghSelect = 0">
                <!-- Youtube dark icon -->
                <img src="../assets/images/yt-icon-light.png" alt="Youtube icon"
                class="hidden dark:flex h-[32px] md:hover:-translate-y-1 transition ease-in-out" 
                :class="ghOpacity.ytCss" draggable="false">
                <!-- Youtube light icon -->
                <img src="../assets/images/yt-icon-dark.png" alt="Youtube icon"
                class="flex dark:hidden h-[32px] md:hover:-translate-y-1 transition ease-in-out" 
                :class="ghOpacity.ytCss" draggable="false">
            </a>
        </div>
      </div>
</template>