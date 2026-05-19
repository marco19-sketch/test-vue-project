<template>
  <div>
    <h2>This is the the component 'TheMultiline'</h2>
    <p>What you type inside the box, will appear underneath:</p>
    <textarea v-model="message" placeholder="text inserted appears above"></textarea>
    <p>{{ message }}</p>
  </div>
</template>
<script setup>
import { ref } from 'vue'
const message = ref('')
</script>

<style scoped>
div {
  border: 2px solid blue;
  border-radius: 10px;
  padding: 20px;
  width: 500px;
  margin: auto;
}
</style>
