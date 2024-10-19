<script setup>
import { ref } from 'vue'
const cityName = ref('')
const breweryData = ref([])

async function handleSearch() {
  let filteredName = cityName.value.trim().toLowerCase()
  const token = localStorage.getItem('token')
  const url = `http://localhost:8000/api/search_city/${filteredName}`
  const headers = {
    'Content-Type': 'application/json',
    Authorization: `Bearer ${token}`,
  }
  try {
    const response = await fetch(url, {
      method: 'GET',
      headers: headers,
    })
    if (!response.ok) {
      alert(`Search failed with status ${response.status}`)
    }
    const json = await response.json()
    breweryData.value = json['data']
    return
  } catch (e) {
    alert(e)
    return
  }
}
</script>

<template>
  <div class="greetings">
    <input v-model="cityName" placeholder="Enter City" required minlength="4" />
    <button @click="handleSearch">Search</button>
  </div>
  <div v-if="breweryData.length > 0">
    <p>yeee</p>
    <div v-for="brew in breweryData" :key="brew.id">
      <h1>{{ brew.name }}</h1>
      <h3>{{ brew.city }}</h3>
    </div>
  </div>
</template>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  position: relative;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}

.greetings h1,
.greetings h3 {
  text-align: center;
}

@media (min-width: 1024px) {
  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}
</style>
