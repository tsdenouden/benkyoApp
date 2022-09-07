<script setup>
import taskList from './components/taskList.vue'
import timer from './components/timer.vue'
import navBar from './components/navBar.vue'

document.title = "Benkyou"

// Request permission for notifications
Notification.requestPermission()

</script>

<template>
  <div class="min-w-screen min-h-screen max-w-full max-h-full
  backdrop-filter backdrop-blur-md bg-white bg-opacity-90 
  dark:bg-zinc-900 dark:bg-opacity-75">
    <router-view></router-view>
  </div>
</template>

<style>

body {
  background-image: url(assets/images/bgimage.jpg);
  background-size: cover;
}


html.dark {
  color-scheme: dark;
}

</style>