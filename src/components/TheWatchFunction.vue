<script setup>
import { ref, watch } from 'vue'

const question = ref('')
const answer = ref('Questions usually contain a question mark. ;-)')
const loading = ref(false)

// watch works directly on a ref
watch(question, async (newQuestion) => {
  if (newQuestion.includes('?')) {
    loading.value = true
    answer.value = 'Thinking...'
    try {
      const res = await fetch('https://yesno.wtf/api')
      answer.value = (await res.json()).image
    } catch (error) {
      answer.value = 'Error! Could not reach the API. ' + error
    } finally {
      loading.value = false
    }
  }
})

</script>

<template>
  <div>
  <h2>This is the 'TheWatchFunction' component</h2>
  <h3>It watches if an '?' is included in the question</h3>
  <h3>if it is the answer will show up</h3>
  <p>
    Ask a yes/no question:
    <input v-model="question" :disabled="loading" />
  </p>
  <img :src="answer" alt="" />
  </div>
</template>

<style scoped>
div {
  border: 2px solid black;
  border-radius: 20px;
  margin: 20px auto;
  padding: 20px;
  width: 500px;
}
</style>
