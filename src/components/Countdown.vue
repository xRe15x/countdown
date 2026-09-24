<script setup>
import { ref, computed, reactive } from 'vue';

import CountdownUnit from './CountdownUnit.vue';
import CountdownButton from './CountdownButton.vue';

let time = reactive({
    second: 5,
    minute: 1,
    hour: 0,
    day: 0
})

const indexTime = ["second", "minute", "hour", "day"];
let running = ref(false);
let lastTime = 0;

function start() {
    console.log("Start");
    running.value = true;
}

function stop() {
    console.log("Stop");
    running.value = false;
}

function decreaseTime() {
    const nonZero = Object.values(time).findIndex((v) => v > 0);
    if (nonZero === -1) return;

    indexTime.slice(0, nonZero).forEach((v) => {
        time[v] = v === "hour" ? 23 : 59;
    });

    time[indexTime[nonZero]] -= 1;
    // console.log(
    //     `${time.day}:${time.hour}:${time.minute}:${time.second} - Value: ${time[indexTime[nonZero]]}, Index: ${indexTime[nonZero]}`,
    // );
}

const getDay = computed(() => String(Math.floor(time.day)).padStart(2, "0"));
const getHour = computed(() => String(Math.floor(time.hour)).padStart(2, "0"));
const getMinute = computed(() => String(Math.floor(time.minute)).padStart(2, "0"));
const getSeconds = computed(() => String(time.second).padStart(2, "0"));

setInterval(() => {
    if (running.value == false) return;

    if (Date.now() - lastTime >= 1000) {
        decreaseTime();
        lastTime = Date.now();
    }
}, 20);
</script>

<template>
    <div class="countdown">
        <div class="time-container">
            <CountdownUnit v-model="getDay" :isReadOnly="running" unit="day" separator></CountdownUnit>
            <CountdownUnit v-model="getHour" :isReadOnly="running" unit="hour" separator></CountdownUnit>
            <CountdownUnit v-model="getMinute" :isReadOnly="running" unit="minute" separator></CountdownUnit>
            <CountdownUnit v-model="getSeconds" :isReadOnly="running" unit="seconds"></CountdownUnit>
        </div>

        <div class="buttons">
            <CountdownButton @click="start">Start</CountdownButton>
            <CountdownButton @click="stop">Stop</CountdownButton>
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