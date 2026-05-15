<template>
    <span>Multiline message is:</span>
    <p>{{ message }}</p>
    <textarea v-model="message" placeholder="text inserted appears above"></textarea>
</template>
<script setup>
import { ref } from 'vue'
const message = ref('')
</script>

<style scoped></style>
