<script setup>
import { ref, computed } from 'vue';

import CountdownUnit from './CountdownUnit.vue';
import CountdownButton from './CountdownButton.vue';

let time = ref(2); // In seconds

function start() {
    console.log("Start");
}

function stop() {
    console.log("Stop");
}

function set() {
    console.log("Set");
}

setInterval(() => {

}, 20);
</script>

<template>
    <div class="countdown">
        <div class="time-container">
            <CountdownUnit unit="day" separator>
                {{ String(Math.floor(time / 86400)).padStart(2, "0") }}
            </CountdownUnit>

            <CountdownUnit unit="hour" separator>
                {{ String(Math.floor(time / 3600) % 24).padStart(2, "0") }}
            </CountdownUnit>

            <CountdownUnit unit="minute" separator>
                {{ String(Math.floor(time / 60) % 60).padStart(2, "0") }}
            </CountdownUnit>

            <CountdownUnit unit="seconds">
                {{ String(time % 60).padStart(2, "0") }}
            </CountdownUnit>
        </div>

        <div class="buttons">
            <CountdownButton @click="start">Start</CountdownButton>
            <CountdownButton @click="stop">Stop</CountdownButton>
            <CountdownButton @click="set">Set</CountdownButton>
        </div>
    </div>
</template>

<style scoped>
.countdown {
    background-color: var(--countdown-colour);
    padding: 1.5rem;
    border-radius: 20px;
    border: 2px solid var(--border-colour);
}

.time-container {
    display: flex;
}

.buttons {
    display: flex;
    justify-content: center;
    align-items: center;
    margin-top: 1rem;
    gap: 0.5rem;
}
</style>