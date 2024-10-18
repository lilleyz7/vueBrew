<script setup>
import { ref } from 'vue'

const emit = defineEmits(['response', 'error'])
const username = ref('')
const password = ref('')

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
      emit('error', response.json())
    }

    const successfulJson = await response.json()
    emit('response', successfulJson)
    return
  } catch (e) {
    alert(e)
  }
}
</script>

<template>
  <div className="form-container">
    <h2>Login</h2>
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

      <p>Don't have an account? register<a href="/register">HERE</a></p>
    </form>
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
