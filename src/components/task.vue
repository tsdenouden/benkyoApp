<script setup>
const { computed, ref, reactive }=require("@vue/runtime-core")

const props = defineProps ({
    textContent: String
})

// state of task's completion, true = task completed
const taskState = ref(false)


// change task item properties based on task state
const taskProps = computed(() => {
    
    let task = reactive({
        // radio circle css
        outerCircle: String,
        innerCircle: String,

        // input field
        inputDisabled: Boolean
    })
    
    if (taskState.value === true) {
        task.outerCircle = "border-zinc-600 hover:bg-zinc-300 dark:hover:bg-zinc-800"
        task.innerCircle = "bg-zinc-600"

        task.inputDisabled = true
    } else {
        task.outerCircle = "border-sky-500 hover:bg-sky-100 dark:hover:bg-sky-900"
        task.innerCircle = "bg-transparent"

        task.inputDisabled = false
    }

    return task
})


</script>

<template>
    <!-- task item -->
    <div class="flex justify-left items-center border-2 rounded-lg 
    w-[90vw] md:w-[45vw] h-auto transition ease-in-out duration-300 m-1 p-5"
    :class="(taskState === true)?'border-zinc-600':'border-sky-500'">

        <!-- outer circle -->
        <div @click="taskState = !taskState" class="border-2 rounded-full
        transition ease-in-out duration-300 mr-4 p-1" :class="taskProps.outerCircle">

            <!-- inner circle -->
            <div class="rounded-full transition ease-in-out 
            duration-300 p-4" :class="taskProps.innerCircle"></div>
        </div>

        <!-- task description -->
        <div class="truncate w-full">
            
            <span class="w-full" :class="(taskState === true)? 'italic line-through text-zinc-600': ''">
                
                <input v-if="!taskProps.inputDisabled" type="text" v-model="textContent" 
                class="bg-transparent border-b-2 border-sky-500
                focus:outline-none focus:bg-zinc-100 dark:focus:bg-zinc-800 
                w-full" placeholder="Untitled task">

                <p v-if="taskProps.inputDisabled">{{ textContent }}</p>
            
            </span>
        
        </div>
    </div>
</template>