<template>
  <div class="widget">
    <h2 class="widget-title">Widget Lokasi</h2>
    <div class="location-input">
      <div class="input-item">
        <label for="latitude">Latitude:</label>
        <input id="latitude" v-model="latitude" type="number" step="0.000001">
      </div>
      <div class="input-item">
        <label for="longitude">Longitude:</label>
        <input id="longitude" v-model="longitude" type="number" step="0.000001">
      </div>
      <button @click="getCityName">Cari Lokasi</button>
    </div>
    <div class="location-info">
      <div class="location-item">
        <span class="label">Lokasi:</span>
        <span class="value">{{ location }}</span>
      </div>
      <div class="location-item">
        <span class="label">Latitude:</span>
        <span class="value">{{ latitude }}</span>
      </div>
      <div class="location-item">
        <span class="label">Longitude:</span>
        <span class="value">{{ longitude }}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'LocationWidget',
  data() {
    return {
      location: '',
      latitude: 0,
      longitude: 0
    }
  },
  methods: {
    getCityName() {
      const url = `https://api.bigdatacloud.net/data/reverse-geocode-client?latitude=${this.latitude}&longitude=${this.longitude}&localityLanguage=en`
      fetch(url)
        .then(response => response.json())
        .then(data => {
          this.location = data.city
        })
        .catch(error => {
          console.log(error)
        })
    }
  }
}
</script>

<style scoped>
.widget {
  margin: 20px;
  padding: 20px;
  border: 1px solid #ccc;
  background-color: #f5f5f5;
  border-radius: 5px;
}

.widget-title {
  font-size: 18px;
  margin-bottom: 10px;
  color: #42b983;
}

.location-input {
  display: flex;
  align-items: center;
  margin-bottom: 10px;
}

.input-item {
  margin-right: 10px;
}

.input-item label {
  font-weight: bold;
}

.location-info {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 10px;
}

.location-item {
  display: flex;
  align-items: center;
}

.label {
  font-weight: bold;
  margin-right: 5px;
  color: #42b983;
}

.value {
  font-size: 16px;
  color: #333;
}
</style>
