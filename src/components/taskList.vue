<script setup>
import { reactive, ref } from '@vue/runtime-core'
import task from './task.vue'


// current task id
var current_Task = 4

var tasks = reactive([
    {
        "id": 1,
        "content": "Example Task 3"
    },
    {
        "id": 2,
        "content": "Example Task 2"
    },
    {
        "id": 3,
        "content": "Example Task 1"
    },
])


const userInput = ref('')

// pushes a new non-empty task object to tasks array
const pushTask = () => {
    if (userInput.value.trim() != '') {
        let newTask = {
            "id": current_Task,
            "content": userInput.value
        }
        tasks.push(newTask)
        current_Task += 1
        userInput.value = ''
    }

}

const submitTask = (e) => {
    if (e.key === 'Enter') {
        pushTask()
    }
}


const taskRemove = (taskId) => {
    const objIndex = tasks.findIndex(obj => {
        return obj.id === taskId
    })
    tasks.splice(objIndex, 1)
}


const clearTasks = () => {
    tasks.length = 0
}

</script>

<template>
    <br>
    <div class="flex flex-col justify-center items-center">
        <!-- Input Field for entering new tasks -->
        <div class="flex flex-row items-center">
            <input type="text" v-model="userInput" @keyup="submitTask" 
            placeholder="Add a new task" class="bg-zinc-100 dark:bg-zinc-900
            dark:text-white border-2 border-sky-500 focus:outline-none 
            rounded-lg mb-3 p-5">

            <!-- Send button -->
            <div @click="pushTask" class="bg-sky-500 rounded-full select-none
            border-4 border-transparent hover:border-sky-200 dark:hover:border-sky-600
            transition ease-in-out duration-100 p-3 ml-3 mb-3">
                <img src="../assets/images/send-plane-2-dark.png" alt="Send message"
                class="hidden dark:flex" draggable="false">
                <img src="../assets/images/send-plane-2-light.png" alt="Send message"
                class="flex dark:hidden" draggable="false">
            </div>
        </div>

        <!-- List of tasks -->
        <div v-for="task in tasks.slice().reverse()" :key="task.id">
            <div v-motion-pop class="flex">
                <task :textContent="task.content"/>

                <!-- Delete individual tasks (Not available for mobile) -->
                <button @click="taskRemove(task.id)"
                class="hidden md:flex md:items-center
                bg-transparent border-2 border-red-200 rounded-lg 
                hover:bg-red-300 dark:hover:bg-red-800 dark:hover:bg-opacity-30
                transition ease-in-out duration-300 m-2 p-5">🗑️</button>
            </div>
        </div>

        <!-- Clear all tasks -->
        <div @click="clearTasks" class="text-white font-bold
        bg-sky-500 hover:bg-sky-400 rounded-lg p-5 m-5">Clear all tasks</div>
    </div>
</template>