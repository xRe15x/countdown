<script setup>
import CountdownSeparator from './CountdownSeparator.vue';

const modelValue = defineModel();

defineProps({
    unit: String,
    separator: Boolean,
    isReadOnly: Boolean
})
</script>

<template>
    <div class="countdown-unit">
        <input type="text" class="time" v-model="modelValue" :readonly="isReadOnly">
        <CountdownSeparator v-if="separator" />
        <div v-else></div>
        <div class="unit">{{ unit }}</div>
    </div>
</template>

<style scoped>
.countdown-unit {
    font-size: 5rem;
    display: grid;
    grid-template: 1fr auto / auto auto;
}

.unit {
    font-size: 0.3em;
    text-align: center;
    color: var(--text2-colour);
}

.time {
    background-color: transparent;
    border: none;
    font-size: inherit;
    width: 5.5rem;
}
</style>