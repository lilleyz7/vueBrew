<script setup>
import { ref } from 'vue'
const username = ref('')
const password = ref('')
const password2 = ref('')
const email = ref('')

const emit = defineEmits(['response', 'error'])

function navigateToLogin() {
  emit('response', 1)
}
async function handleRegister() {
  if (password.value !== password2.value) {
    alert('Passwords do not match')
    return
  }
  const url = 'http://localhost:8000/auth/register/'
  const data = {
    username: username.value,
    email: email.value,
    password: password.value,
  }
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
    localStorage.setItem('token', successfulJson.access)
    emit('response', 0)
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
        required
      />

      <label>Email</label>
      <input v-model="email" type="email" id="email" name="email" required />

      <label>Password</label>
      <input
        v-model="password"
        type="password"
        id="password"
        name="password"
        required
      />

      <label>Enter Password Again</label>
      <input
        v-model="password2"
        type="password"
        id="password2"
        name="password2"
        required
      />
      <button @click="handleRegister" type="submit">Register</button>
    </form>
  </div>
  <p>
    Already have an account?
    <button @click="navigateToLogin">Login Here</button>
  </p>
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
