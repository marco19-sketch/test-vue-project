<template>
    <button @click="warn('test warning', $event)">Test event</button>
    <p>{{ warnReturnValue }}</p>
</template>
<script setup>
import { ref } from 'vue'

    const warnReturnValue = ref('')

    const warn = (message, event) => {
        console.log(message, event.layerX)
        warnReturnValue.value = `cursor position at click coordinates: X:${event.layerX} Y:${event.layerY}`;
    }
</script>
<style scoped></style>