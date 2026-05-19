<template>
  <div>
    <h2>This is the 'TheEvent' component</h2>
    <p>Clicking the button will tell the cursor position coordinates</p>
    <button @click="warn('test warning', $event)">Test event</button>
    <p>{{ warnReturnValue }}</p>
  </div>
</template>
<script setup>
import { ref } from 'vue'

const warnReturnValue = ref('')

const warn = (message, event) => {
  console.log(message, event.layerX)
  warnReturnValue.value = `cursor position at click coordinates: X:${event.layerX} Y:${event.layerY}`
}
</script>
<style scoped>
div {
  margin: 30px auto;
  border: 2px solid green;
  width: 500px;
  padding: 20px;
  border-radius: 20px;
}
</style>
