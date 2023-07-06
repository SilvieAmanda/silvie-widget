<template>
  <div class="widget">
    <h2>Widget Cuaca</h2>
    <div class="search-container">
      <input v-model="searchQuery" placeholder="Masukkan lokasi">
      <button @click="searchWeather">Cari</button>
    </div>
    <div v-if="weatherData" class="weather-info">
      <div class="weather-icon">
        <img :src="getWeatherIconUrl(weatherData.weather[0].icon)" :alt="weatherData.weather[0].description" />
      </div>
      <div class="weather-details">
        <h3>{{ weatherData.name }}</h3>
        <p class="description">{{ weatherData.weather[0].description }}</p>
        <p class="temperature">{{ weatherData.main.temp }}°C</p>
      </div>
    </div>
    <div v-else class="loading-message">Loading...</div>
  </div>
</template>


<script>
export default {
  name: 'WeatherWidget',
  data() {
    return {
      weatherData: null,
      apiKey: 'c3cf95ac472efcf8dbe44c52f848b83b',
      searchQuery: ''
    }
  },
  methods: {
    searchWeather() {
      const url = `https://api.openweathermap.org/data/2.5/weather?q=${this.searchQuery}&units=metric&appid=${this.apiKey}`
      fetch(url)
        .then(response => response.json())
        .then(data => {
          this.weatherData = data
        })
        .catch(error => {
          console.log(error)
        })
    },
    getWeatherIconUrl(icon) {
      return `https://openweathermap.org/img/wn/${icon}.png`
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

h2 {
  color: #42b983;
  margin-bottom: 10px;
}

.search-container {
  display: flex;
  align-items: center;
  margin-bottom: 10px;
}

.search-container input {
  width: 200px;
  padding: 5px;
  border: 1px solid #ccc;
  border-radius: 3px;
}

.search-container button {
  padding: 5px 10px;
  background-color: #42b983;
  color: #fff;
  border: none;
  border-radius: 3px;
  cursor: pointer;
}

.weather-info {
  display: flex;
  align-items: center;
}

.weather-icon {
  margin-right: 20px;
}

.weather-icon img {
  width: 50px;
}

.weather-details {
  color: #333;
}

.description {
  font-weight: bold;
}

.temperature {
  font-size: 24px;
}

.loading-message {
  text-align: center;
  color: #42b983;
  font-style: italic;
}
</style>
