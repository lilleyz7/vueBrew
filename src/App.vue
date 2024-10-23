<script setup>
import { onMounted, ref, watch } from 'vue'
import LoginView from './components/LoginView.vue'
import RegisterView from './components/RegisterView.vue'
import SearchView from './components/SearchView.vue'

const currentView = ref(1)
const token = ref(null)
const success = ref(null)
const error = ref(null)

watch(currentView, () => {
  token.value = localStorage.getItem('access')
})
watch(error, () => {
  success.value = null
})

async function logout() {
  await localStorage.removeItem('access')
  token.value = null
  currentView.value = 1
}

onMounted(() => {
  const tokenFromStorage = localStorage.getItem('access')
  if (tokenFromStorage) {
    token.value = tokenFromStorage
    currentView.value = 0
  }
})
</script>

<template>
  <main>
    <div v-if="token">
      <button @click="currentView = 0">Home</button>
      <button @click="logout">Logout</button>
      <button @click="currentView = 3">Search</button>
      <div v-if="currentView === 3">
        <SearchView />
      </div>
      <!-- <div v-else-if="currentView === 0">
        <SavesView />
      </div> -->
    </div>
    <div v-else>
      <ul>
        <li><button @click="currentView = 1">Login</button></li>
        <li><button @click="currentView = 2">Register</button></li>
      </ul>
    </div>
    <div v-if="currentView === 1 && !token">
      <LoginView
        @response="res => (currentView = res)"
        @error="err => (error = err)"
      />
    </div>
    <div v-else-if="currentView === 2 && !token">
      <RegisterView
        @response="res => (currentView = res)"
        @error="err => (error = err)"
      />
    </div>
  </main>
</template>
