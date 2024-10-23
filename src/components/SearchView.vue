<script setup>
import { ref } from 'vue'
import TableComponent from './TableComponent.vue'
const cityName = ref('')
const breweryData = ref([])
const searched = ref(false)

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
    searched.value = true
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
  <div v-if="searched">
    <TableComponent :breweries="breweryData" />
  </div>
</template>

<style scoped></style>
