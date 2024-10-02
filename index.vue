<script setup>
// Import necessary Vue functions
import { ref, onMounted } from 'vue'

// Define a reactive variable to hold the music data
const musicData = ref([])

// Fetch JSON data when the component is mounted using axios
onMounted(async () => {
  try {
    const response = await uni.request({
      method: 'GET',
      url: 'https://ongeki.sega.jp/assets/json/music/music.json',
    })
    musicData.value = response.data
  } catch (error) {
    console.error('Error fetching music data:', error)
  }
})
</script>

<template>
  <!-- Card list container -->
  <div class="d-flex justify-content-center">
    <ul class="list-unstyled">
      <li v-for="(music, index) in musicData" :key="index" class="mb-4">
        <div class="card" style="width: 18rem;">
          <!-- Placeholder for an image -->
          <img :src="'https://ongeki-net.com/ongeki-mobile/img/music/' + music.image_url" class="card-img-top" alt="Music cover image">
          <div class="card-body">
            <!-- Title and artist from the JSON data -->
            <h5 class="card-title">{{ music.title }}</h5>
            <p class="card-subtitle text-muted">{{ music.artist }}</p>
            <span class="badge rounded-pill text-bg-secondary">{{ music.category }}</span>
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
