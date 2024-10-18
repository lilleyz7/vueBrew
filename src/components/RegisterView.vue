<script setup>
import { ref } from 'vue'
const username = ref('')
const password = ref('')
const password2 = ref('')

function handleRegister() {}
</script>

<template>
  <div className="form-container">
    <h2>Login</h2>
    <form method="POST">
      <label>Username</label>
      <input
        v-model="username"
        type="text"
        id="username"
        name="username"
        required
      />

      <label>Password</label>
      <input
        v-model="password"
        type="password"
        id="password"
        name="password"
        required
      />
      <button @click="handleRegister" type="submit">Login</button>

      <label>Enter Password Again</label>
      <input
        v-model="password2"
        type="password"
        id="password2"
        name="password2"
        required
      />
      <button type="submit">Login</button>

      <p>Already have an account? Login<a href="/login">HERE</a></p>
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
