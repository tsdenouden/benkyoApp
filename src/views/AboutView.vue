<script setup>
    import navBar from '../components/navBar.vue'

    document.title = "About Benkyou"
</script>

<template>
    <navBar linkHref="/" linkMsg="Home" />
    <div v-motion-fade class="lg:w-1/2 mx-3 lg:mx-32 p-10">
        
        <div class="mb-4 lg:mb-10">
            <div class="mb-1">
                <span class="font-bold text-2xl"><h1>What is Benkyou?</h1></span>
            </div>
            <div class="mx-3">
                <p>Benkyou is a <span class="font-bold">Pomodoro</span> web app.</p>
                <p>It's a simple implementation of a Pomodoro timer with a few things
                    I wanted.
                </p>
                <div class="mt-3 md:mt-0">
                    <p>My primary reason for making this was simply to practice using Vue.js
                        since i'm still very very new to it.
                    </p>
                </div>
            </div>
        </div>

        <div class="mb-4 lg:mb-10">
            <div class="pb-1">
                <span class="font-bold text-2xl"><h1>What is a Pomodoro?</h1></span>
            </div>
            <div class="mx-3">
                <p> 
                    <span class="text-sky-900 dark:text-sky-600">
                        <a href="https://en.wikipedia.org/wiki/Pomodoro_Technique" target="_blank" 
                        rel="noopener noreferrer">
                            Wikipedia:
                        </a>
                    </span> 
                    "The Pomodoro Technique is a time management method developed by 
                    Francesco Cirillo in the late 1980s. It uses a kitchen timer to 
                    break work into intervals, typically 25 minutes in length, separated 
                    by short breaks."
                </p>
                <br>
                <p>
                    Basically, everytime you complete a 25 minute study session, follow
                    it up with a 5 minute short break. This counts as one Pomodoro.
                    After 4 Pomodoros, take a 15 minute long break. Good luck studying!
                </p>
            </div>
        </div>

        <div>
            <div>
                <span class="font-bold text-2xl"><h1>Who is @tsdenouden?</h1></span>
            </div>
            <div class="mx-3">
                <p> 
                    Hi! I'm Tristan and I'm pretty new to web development.
                    This is my first time using a JS framework. Prior to this, I made
                    <a href="https://github.com/tsdenouden/enoto-markdown" target="_blank"
                    rel="noopener noreferrer" class="text-sky-900 dark:text-sky-600">Enoto</a>, a 
                    web-based Markdown editor with Flask. At the moment, I'm just learning
                    random stuff for fun and to build up my frontend skills. If you'd like
                    to contact me, you can shoot me a message on 
                    <a href="https://www.behance.net/tristandenouden" target="_blank"
                    rel="noopener noreferrer" class="text-sky-900 dark:text-sky-600">Behance</a>.
                </p>
                <br>
                <br>
                <div class="text-sky-900 dark:text-sky-600 underline">
                    <router-link to="/">Go back</router-link>
                </div>
            </div>
        </div>

    </div>
</template>