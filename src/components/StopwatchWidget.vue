<template>
  <div class="widget">
    <h2 class="widget-title">Widget Stopwatch</h2>
    <div class="time-container">
      <div class="time">{{ formattedTime }}</div>
    </div>
    <div class="buttons-container">
      <button @click="start" :disabled="running">Start</button>
      <button @click="stop" :disabled="!running">Stop</button>
      <button @click="reset" :disabled="running">Reset</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'StopwatchWidget',
  data() {
    return {
      time: 0,
      running: false,
      intervalId: null
    }
  },
  computed: {
    formattedTime() {
      const hours = Math.floor((this.time / 1000 / 60 / 60) % 24)
      const minutes = Math.floor((this.time / 1000 / 60) % 60)
      const seconds = Math.floor((this.time / 1000) % 60)
      const milliseconds = Math.floor((this.time % 1000) / 10)
      return `${this.padNumber(hours)}:${this.padNumber(minutes)}:${this.padNumber(seconds)}.${this.padNumber(milliseconds)}`
    }
  },
  methods: {
    start() {
      if (!this.running) {
        this.intervalId = setInterval(() => {
          this.time += 10
        }, 5)
        this.running = true
      }
    },
    stop() {
      if (this.running) {
        clearInterval(this.intervalId)
        this.intervalId = null
        this.running = false
      }
    },
    reset() {
      this.time = 0
    },
    padNumber(number) {
      return number.toString().padStart(2, '0')
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
}

.time-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100px;
}

.time {
  font-size: 48px;
  position: relative;
  animation: scale 1s infinite;
}

@keyframes scale {
  0% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.1);
  }
  100% {
    transform: scale(1);
  }
}

.buttons-container {
  display: flex;
  justify-content: center;
  margin-top: 20px;
}

button {
  padding: 10px 20px;
  font-size: 16px;
  background-color: #007bff;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

button:disabled {
  background-color: #ccc;
  cursor: not-allowed;
}
</style>
