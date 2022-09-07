<script setup>
const { computed, ref }=require("@vue/runtime-core")

// timer select, values in ms
const durationSelect = { pomodoro: 1500, short: 300, long: 900}


//const durationSelect = { pomodoro: 2, short: 1, long: 5}


// toggle timer
var timerOn = false
const pauseBtn = ref("Start")

const toggleTimer = () => {
    timerOn = !timerOn
    switch (timerOn) {
        case (true):
            pauseBtn.value = "Stop"
            break
        case (false):
            pauseBtn.value = "Start"
            break
    }
}


const countDown = ref(durationSelect.pomodoro)

const pomoTimer = () => {
    if (countDown.value <= 0) {
        // notify user of completed session if they're on a different webpage
        if (document.visibilityState !== "visible") {
            let sessionComplete = new Notification("Benkyou", {
                    body: "Session complete!",
                    icon: ""
                })
        }
        // *auto* reset timer
        resetTimer(currentDuration.value, true)
    } else {
        if (timerOn != false) {
            countDown.value -= 1
        }   
    }
}

var newTimer = setInterval(pomoTimer, 1000)


// currentDuration -> used to check which timer is currently being used
let pomodoroCount = 0
let breakCheck = false
const currentDuration = ref(durationSelect.pomodoro)

const resetTimer = (newDuration, autoReset=false) => {
    clearInterval(newTimer)

    // auto reset, overrides newDuration argument
    if (autoReset === true) {
        // check if user just completed a pomodoro session
        if (currentDuration.value === durationSelect.pomodoro) {
            pomodoroCount += 1
            breakCheck = true
        } else {
            breakCheck = false
        }
        // change new duration after x amount of pomodoros
        switch (pomodoroCount) {
            case 4:
                newDuration = durationSelect.long
                pomodoroCount = 0
                break
            default:
                if (breakCheck === true) {
                    newDuration = durationSelect.short
                } else {
                    newDuration = durationSelect.pomodoro
                }
                break
        }
    }

    // update
    countDown.value = newDuration
    currentDuration.value = newDuration
    newTimer = setInterval(pomoTimer, 1000)

    // pause timer
    timerOn = false
    pauseBtn.value = "Start"
}


// formatting ms into m:s
const timerDisplay = computed(() => {
    let min = Math.floor(countDown.value / 60)
    let sec = countDown.value - (min * 60)
    
    // format seconds to have leading zeroes if < 2 digits
    sec = sec.toString()
    if (sec.length < 2) {
        sec = "0" + sec
    }

    document.title = min.toString() + ":" + sec + " | Benkyou"

    return { min, sec }
})


</script>

<template>
    <div class="flex flex-col justify-center text-center items-center font-mono">
        <!-- Timer Select: Pomodoro Session, Short break, Long break -->
        <div class="flex flex-row items-center text-sm text-black dark:text-white mb-10">
            <div @click="resetTimer(durationSelect.pomodoro)"
            class="grow bg-sky-200 hover:bg-sky-300 dark:bg-sky-700 dark:hover:bg-sky-900
            rounded-md px-5 py-3 mx-3">
                Pomodoro<br>Session
            </div>
            
            <div @click="resetTimer(durationSelect.short)"
            class="grow bg-sky-200 hover:bg-sky-300 dark:bg-sky-700 dark:hover:bg-sky-900
            rounded-md px-5 py-3 mx-3">
                Short<br>break
            </div>

            <div @click="resetTimer(durationSelect.long)"
            class="grow bg-sky-200 hover:bg-sky-300 dark:bg-sky-700 dark:hover:bg-sky-900
            rounded-md px-5 py-3 mx-3">
                Long<br>break
            </div>
        </div>
        <!-- Timer Display  -->
        <div class="text-7xl border-b-4 border-black dark:border-zinc-100">
            {{ timerDisplay.min }}:{{ timerDisplay.sec }}
        </div>
        <br>
        <!-- Control buttons -->
        <div class="flex flex-row text-2xl">
            <button @click="toggleTimer" class="text-black dark:text-white
            border-4 border-sky-400 rounded-full hover:bg-sky-500
            hover:text-zinc-100 dark:hover:text-zinc-800
            transition ease-in-out duration-200
            px-5 py-3 m-3">{{ pauseBtn }}</button>

            <button @click="resetTimer(currentDuration)" class="text-black dark:text-white
            border-4 border-sky-400 rounded-full hover:bg-sky-500
            hover:text-zinc-100 dark:hover:text-zinc-800
            transition ease-in-out duration-200
            px-5 py-3 m-3">Reset</button>
        </div>
        
    </div>
</template>