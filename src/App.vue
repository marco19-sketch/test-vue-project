<script setup>
import { reactive, ref } from 'vue'
//######### REACTIVE API (works only on objects)#############
const counter = reactive({
  val: 0,
})

// ######## REF API (works on any value type)##############
const message = ref('Hello World!')
const titleClass = ref('title')
const count = ref(0)
const text = ref('')
// ######## EVENT LISTENER  #################
function increment(){
  count.value++
}
</script>

<template>
  <!-- v-bind:class='titleClass' directive -->
  <!-- :class is the argument -->
  <!-- in this case "titleClass" is bound to ref('title') -->
  <h1 :class="titleClass">You did it!</h1>
  <p>
    Visit <a href="https://vuejs.org/" target="_blank" rel="noopener">vuejs.org</a> to read the
    documentation
  </p>
  <p>{{ message.toLowerCase() }}</p>
  <p>{{ message.toUpperCase() }}</p>
  <p>{{ counter.val }}</p>
  <button @click="increment">Count is: {{ count }}</button>
  <p>To bound the input and the p below I'm using the v-model directive</p>
  <ul>In order to work it needs:
    <li>a ref variable: <code>const text = ref('')</code></li>
    <li>the v-model on the ref variable: <code>v-model='text'</code></li>
    <li>a target element, in this case it is a: <pre v-pre><code>&lt;p&gt;{{ text }}&lt;/p&gt;</code></pre></li>
  </ul>
  <input id='v-model' v-model="text">
  <p>{{ text }}</p>
</template>

<style scoped>
.title {
  color: blue;
}
#v-model {
  display: block;
}
pre {
  display: inline;
}
</style>
