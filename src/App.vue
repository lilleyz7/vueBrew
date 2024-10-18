<script setup>
import { onMounted, ref } from 'vue'
import LoginView from './components/LoginView.vue'
import RegisterView from './components/RegisterView.vue'
import SearchView from './components/SearchView.vue'

const currentView = ref(1)
const token = ref(null)

onMounted(() => {
  const tokenFromStorage = localStorage.getItem('token')
  if (tokenFromStorage) {
    token.value = tokenFromStorage
  }
})
</script>

<template>
  <main>
    <ul>
      <li><button @click="currentView = 0">Home</button></li>
      <li><button @click="currentView = 1">Login</button></li>
      <li><button @click="currentView = 2">Register</button></li>
      <li><button @click="currentView = 3">Search</button></li>
    </ul>
    <div v-if="currentView === 1 && !token">
      <LoginView />
    </div>
    <div v-else-if="currentView === 2 && !token">
      <RegisterView />
    </div>
    <div v-else-if="currentView === 3">
      <SearchView />
    </div>
    <div v-else-if="currentView === 4">
      <SearchView />
    </div>
    <div v-else><LoginView /></div>
    <!-- <div v-if="currentView === 4">
      <SavesView />
    </div> -->
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
