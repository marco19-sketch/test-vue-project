<script setup>
import { reactive, ref } from 'vue'
import TheMultiline from './components/TheMultiline.vue'
import TheEvent from './components/TheEvent.vue'
import TheWatchFunction from './components/TheWatchFunction.vue'
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
function increment() {
  count.value++
}

// ############# watch function (this follows the cursor's click positions)#######
const x = ref(0)
const y = ref(0)
const position = (event) => {
    x.value = event.layerX;
    y.value = event.layerY;
}
</script>

<template>
  <body @click="position($event)">
    <h3>Click to see the coordinates of the cursor in the page here : </h3>
        <p class="coords"> X:{{ x }} Y:{{ y }}</p>
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
  <ul>
    In order to work it needs:
    <li>a ref variable: <code>const text = ref('')</code></li>
    <li>the v-model on the ref variable: <code>v-model='text'</code></li>
    <li>
      a target element, in this case it is a:
      <pre v-pre><code>&lt;p&gt;{{ text }}&lt;/p&gt;</code></pre>
    </li>
  </ul>
  <div id="input-container">
    <label for="v-model"
      >Type in the box below
      <input id="v-model" v-model="text" />
    </label>
    <p>{{ text }}</p>
    <TheMultiline />
    <TheEvent />
    <TheWatchFunction />
  </div>
  </body>
</template>

<style scoped>
h3 {
  display: inline;
}
.coords {
  display: inline;
  color: blue;
  font-size: 20px;
}
.title {
  color: blue;
}
#v-model {
  display: block;
}
pre {
  display: inline;
}
#input-container {
  border: 1px, solid, blue;
  width: fit-content;
  padding: 10px;
  border-radius: 10px;
}
</style>
