<script setup>
import { ref, reactive, onMounted } from 'vue'
import axios from 'axios'

const studenti = reactive([])
// const studenti = ref([])
const loading = ref(false)
const nome = ref('')
const cognome = ref('')
const eta = ref(null)
const error = ref(null)
let success = ref('')
// const bodyStudente = reactive({"cognome": null, "nome": null, "eta": null})

//API base URL
// const API_BASE_URL = 'http://localhost:5000/v1/api'
const API_BASE_URL = 'http://localhost:5000'

//Axios instance with config
const apiClient = axios.create({
  baseURL: API_BASE_URL,
  headers: {
    'Content-type': 'application/json'
  }
})

//Methods
const fetchStudenti = async () => {
  loading.value = true
  error.value = null

  try {
    const response = await apiClient.get('/studenti')
    studenti.length = 0
    studenti.push(...response.data)
    // studenti.value = response.data
  } catch (err) {
    error.value = `Errore nel recuperare lista studenti: ${err.message}`
    console.error(err)
  } finally {
    loading.value = false
  }
}

const postStudente = async () => {
  if (cognome.value.trim() === '' || nome.value.trim() === '' || eta.value === null) {
    console.log('Missing field error')
    return 'Uno o più campi sono mancanti'
  }

  try {
    const response = await apiClient.post('/studenti', {
      cognome: cognome.value,
      nome: nome.value,
      eta: eta.value
    })
    studenti.push(response.data)
  } catch (err) {
    error.value = `Errore, non è stato possibile aggiungere lo studente:  ${err.message}`
    console.error(err)
  }
  cognome.value = ''
  nome.value = ''
  eta.value = null
}

const eliminaStudente = async (id) => {
  console.log(id)
  try {
    const response = await apiClient.delete(`/studenti/${id}`)
    const filtered = studenti.filter(s => s.id !== id)
    studenti.length = 0;
    studenti.push(...filtered)
    success.value = response.data.msg
    console.log('success', success.value)
  } catch (err) {
    error.value = `Non è stato possibile eliminare lo studente con id: ${id}: ${err}`
    console.log(err)
  }
}

// Life cycle - fetch studenti when component mounts
onMounted(() => {
  fetchStudenti()
})
</script>

<template>
  <div class="container">
    <h2>Elenco Studenti</h2>
    <div v-if="loading">Loading...</div>
    <table>
      <thead>
        <tr>
          <th class="id">ID</th>
          <th>Cognome</th>
          <th>Nome</th>
          <th>Età</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="studente in studenti" :key="studente.id">
          <td class="id">{{ studente.id }}</td>
          <td>{{ studente.nome }}</td>
          <td>{{ studente.cognome }}</td>
          <td id="eta">{{ studente.eta }}<button type='button' @click='eliminaStudente(studente.id)'>x</button></td>
        </tr>
      </tbody>
    </table>

    <form action="/studenti" method="POST">
      <input type="text" v-model="cognome" placeholder="cognome">
      <input type="text" v-model="nome" placeholder="nome">
      <input type="text" v-model="eta" placeholder="età">
      <button type="submit" @click.prevent="postStudente">Aggiungi Studente</button>
    </form>
    <p class='error-message' v-if="error">{{ error }}</p>
    <p>{{ success }}</p>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  width: fit-content;
  margin: auto;
  align-items: center;
}
table {
  border: 1px solid blue;
  border-collapse: collapse;
}
td, th {
  border: 1px solid blue;
  padding: 5px;
  width: 100px;
}

th {
  height: 30px;
  background-color: rgb(180, 180, 180);
}

.id {
  width: 50px;
}

table #eta {
  display: flex;
  justify-content: right;
}

table #eta button {
  margin-left: 10px;
}

.error-message {
  color: red;
}

form {
  margin: 20px auto;
}

form > input {
  margin: 5px;
}

form > button {
  display: block;
  padding: 5px;
  width: fit-content;
  margin: 10px auto;
}
</style>
