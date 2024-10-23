<script setup>
import { onMounted, ref } from 'vue'
import TableComponent from './TableComponent.vue'

const saveData = ref([])

async function fetchData() {
  const token = localStorage.getItem('token')
  const url = `http://localhost:8000/api/view_saves`
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
    saveData.value = json['data']
    return
  } catch (e) {
    alert(e)
    return
  }
}

onMounted(fetchData)
</script>

<template>
  <h1>Saved Breweries</h1>
  <div><TableComponent :breweries="saveData" /></div>
</template>
