<script setup>
import { onMounted, ref } from 'vue'
import TableComponent from './TableComponent.vue'

const saveData = ref([])
onMounted(async () => {
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
})
</script>

<template>
  <div><TableComponent /></div>
</template>
