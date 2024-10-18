<script setup>
import { ref } from 'vue'
const data = ref(null)

function handleSearch() {}
</script>

<template>
  <div class="greetings"></div>
  <input v-model="data" placeholder="Enter City" />
  <button @click="handleSearch">Search</button>
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
