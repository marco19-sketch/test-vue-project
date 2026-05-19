<script setup>
import { ref, computed } from 'vue'
import Home from './views/HomeView.vue'
import Studenti from './views/StudentiView.vue'
import FunctionsTesting from './views/FunctionsTesting.vue'

// ################# Routing #########################
const routes = {
  '/': Home,
  '/studenti': Studenti,
  '/functions': FunctionsTesting,
}

const currentPath = ref(window.location.hash)

window.addEventListener('hashchange', () => {
  currentPath.value = window.location.hash
})

const currentView = computed(() => {
  return routes[currentPath.value.slice(1) || '/']
})
</script>

<template>
  <!-- routing -->
  <nav>
    <a href="#/">Home</a>
    <a href="#/studenti">Studenti</a>
    <a href="#/functions">Functions Testing</a>
  </nav>
  <component :is="currentView" />
</template>

<style scoped>
nav {
  border: 1px solid transparent;
  width: fit-content;
  margin: auto;
}

a {
  margin: 5px 10px;
}
</style>
