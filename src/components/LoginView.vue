<script setup>
import { ref } from 'vue'

const emit = defineEmits(['response', 'error'])
const username = ref('')
const password = ref('')

async function switchToRegister() {
  emit('response', 2)
}

async function handleLogin() {
  const url = 'http://localhost:8000/auth/token/'
  const data = { username: username.value, password: password.value }
  try {
    const response = await fetch(url, {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify(data),
    })

    if (!response.ok) {
      emit('error', await response.json())
    }

    const successfulJson = await response.json()
    localStorage.setItem('access', successfulJson.access)
    localStorage.setItem('refresh', successfulJson.refresh)
    emit('response', 3)
    return
  } catch (e) {
    alert(e)
  }
}
</script>

<template>
  <div className="form-container">
    <form @submit.prevent="onSubmit" method="POST">
      <label>Username</label>
      <input
        v-model="username"
        type="text"
        id="username"
        name="username"
        :minlength="8"
        :maxlength="20"
        required
      />

      <label>Password</label>
      <input
        v-model="password"
        type="password"
        id="password"
        name="password"
        :minlength="8"
        required
      />
      <button @click="handleLogin" type="submit">Login</button>
    </form>
    <p>
      Don't have an account?
      <button @click="switchToRegister">Register Here</button>
    </p>
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
