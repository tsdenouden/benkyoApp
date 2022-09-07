<script setup>
import taskList from '../components/taskList.vue'
import timer from '../components/timer.vue'
import navBar from '../components/navBar.vue'

document.title = "Benkyou"

// Request permission for notifications
Notification.requestPermission()

</script>

<template>
    <navBar linkHref="/about" linkMsg="About Benkyou" />
    <div v-motion-fade class="flex flex-col justify-center items-center
    p-10">
      <timer />
      <taskList />
    </div>
</template>