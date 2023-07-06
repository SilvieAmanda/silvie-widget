<template>
  <div id="app">
    <h1 class="app-title">Widget App</h1>
    <div class="menu">
      <button :class="{ active: selectedWidget === 'weather' }" @click="selectedWidget = 'weather'">Widget Cuaca</button>
      <button :class="{ active: selectedWidget === 'location' }" @click="selectedWidget = 'location'">Widget Lokasi</button>
      <button :class="{ active: selectedWidget === 'stopwatch' }" @click="selectedWidget = 'stopwatch'">Widget Stopwatch</button>
      <button :class="{ active: selectedWidget === 'game' }" @click="selectedWidget = 'game'">Widget Game</button>
      <button :class="{ active: selectedWidget === 'photo' }" @click="selectedWidget = 'photo'">Widget Foto</button>
    </div>
    <div class="widget-container">
      <component :is="selectedWidget + '-widget'" v-if="selectedWidget" />
    </div>
  </div>
</template>

<script>
import WeatherWidget from './components/WeatherWidget.vue'
import LocationWidget from './components/LocationWidget.vue'
import StopwatchWidget from './components/StopwatchWidget.vue'
import GameWidget from './components/GameWidget.vue'
import PhotoWidget from './components/PhotoWidget.vue'

export default {
  name: 'App',
  components: {
    WeatherWidget,
    LocationWidget,
    StopwatchWidget,
    GameWidget,
    PhotoWidget
  },
  data() {
    return {
      selectedWidget: ''
    }
  }
}
</script>

<style scoped>
#app {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  background: linear-gradient(to right, #7e57c2, #ff4081);
}

.app-title {
  text-align: center;
  color: #fff;
  margin-top: 30px;
  font-size: 32px;
  background: linear-gradient(to right, #7e57c2, #ff4081);
  padding: 20px;
}

.menu {
  display: flex;
  justify-content: center;
  margin-bottom: 20px;
  background: none;
}

.menu button {
  padding: 10px 20px;
  font-size: 16px;
  background-color: transparent;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  margin: 0 5px;
  transition: background-color 0.3s ease;
  outline: none;
}

.menu button.active {
  background-color: #0056b3;
}

.widget-container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 300px;
  background: none;
}

.widget {
  margin: 20px;
  padding: 20px;
  border: 1px solid #ccc;
  background-color: #fff;
  border-radius: 5px;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  animation: fadeIn 0.5s ease;
}

body {
  font-family: 'Arial', sans-serif;
  margin: 0;
  padding: 0;
}

@keyframes fadeIn {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}
</style>

