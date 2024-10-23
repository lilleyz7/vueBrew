<script setup>
defineProps({
  breweries: Array,
})

async function saveBrewery(brew_id) {
  if (brew_id == 0) {
    return
  }
  const url = `http://localhost:8000/api/save_brewery/${brew_id}`
  const token = localStorage.getItem('access')
  const headers = {
    'Content-Type': 'application/json',
    Authorization: `Bearer ${token}`,
  }
  try {
    let response = await fetch(url, {
      method: 'POST',
      headers: headers,
    })
    if (response.status >= 200 && response.status < 300) {
      const data = await response.json()
      alert(data.status)
    } else {
      const data = await response.json()
      alert(data.error)
    }
  } catch (e) {
    alert('Error' + toString(e))
  }
}
</script>

<template>
  <div class="">
    <table class="table">
      <!-- head -->

      <thead>
        <tr>
          <th></th>
          <th>Name</th>
          <th>Address</th>
          <th>Brewery Type</th>
          <th>Phone Number</th>
          <th>Link</th>
        </tr>
      </thead>
      <tbody>
        <tr class="hover" v-for="(brew, idx) in breweries" :key="brew.name">
          <td>{{ idx }}</td>
          <td>
            <button @click="saveBrewery(brew.id)">{{ brew.name }}</button>
          </td>
          <td>{{ brew.street }}</td>
          <td>{{ brew.brewery_type }}</td>
          <td>{{ brew.phone }}</td>
          <td>{{ brew.website_url }}</td>
          <td>
            <a :href="brew.url" target="_blank">{{ brew.url }}</a>
          </td>
          <!-- <td><input type="checkbox" class="checkbox" /></td> -->
        </tr>
      </tbody>
    </table>
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
