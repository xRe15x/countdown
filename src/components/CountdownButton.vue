<template>
    <button>
        <slot>Button</slot>
    </button>
</template>

<style scoped>
button {
    background-color: rgb(20, 20, 20);
    padding: 0.6em;
    border-radius: 8px;
    border: 1px solid var(--border-colour);
    font-size: 1rem;
    min-width: 80px;
}

button:hover {
    background-color: rgb(28, 28, 28);
}
</style>