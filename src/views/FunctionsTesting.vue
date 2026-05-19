<template>
  <body @click="position($event)">
    <h1>Functions Testing Page</h1>
    <div class="coordinates">
      <h3>Click anywhere in the page to see the coordinates of the cursor :</h3>
      <p class="coords">X:{{ x }} Y:{{ y }}</p>
    </div>
    <div class="counter">
      <p>
        Count: {{ counter.val }} (← this value won't increments 'cause reactive works only on
        objects)
      </p>
      <button @click="increment">Counter: {{ count }}</button>
    </div>
    <div class="v-model">
      <h3>The v-model directive</h3>
      <ul>
        In order to work it needs:
        <li>a ref variable: <code>const text = ref('')</code></li>
        <li>the v-model on the input element: <code>v-model='text'</code></li>
        <li>
          a target element, in this case it is a:
          <pre v-pre><code>&lt;p&gt;{{ text }}&lt;/p&gt;</code></pre>
        </li>
      </ul>
      <div id="input-container">
        <label for="v-model"
          >Type in the input and...
          <input id="v-model" v-model="text" placeholder="type here..." />
        </label>
        <p>...watch →{{ text }}</p>
      </div>
    </div>
  </body>
</template>

<script setup>
import { ref, reactive } from 'vue'

// ######## REF API (works on any value type)##############
const text = ref('')

//######### REACTIVE API (works only on objects)#############
const counter = reactive({
  val: 0,
})

// ######## EVENT LISTENER  #################
const count = ref(0)
function increment() {
  count.value++
}

// ############# watch function (this follows the cursor's click positions)#######
const x = ref(0)
const y = ref(0)
const position = (event) => {
  x.value = event.layerX
  y.value = event.layerY
}
</script>

<style scoped>
h1 {
  text-align: center;
}
.coordinates {
  border: 1px dotted red;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 60%;
  border-radius: 20px;
  margin: auto;
}
.coordinates > p {
  font-size: 1.5rem;
  margin-left: 20px;
}

.counter {
  border: 1px dotted green;
  margin: 20px auto;
  width: 600px;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px;
  border-radius: 20px;
}

.counter > button {
  padding: 10px;
  border-radius: 5px;
  background-color: green;
  color: white;
}

.v-model {
  border: 1px dotted blue;
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 50%;
  margin: auto;
  border-radius: 20px;
}

#input-container input {
  padding: 5px;
  border-radius: 5px;
}
</style>
