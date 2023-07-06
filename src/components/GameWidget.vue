<template>
  <div class="widget">
    <h2>Widget Game</h2>
    <div class="game-container">
      <div class="hole" v-for="(mole, index) in moles" :key="index" @click="hitMole(index)">
        <div class="mole" v-if="mole.show"></div>
      </div>
    </div>
    <div class="score">Score: {{ score }}</div>
    <div class="time">Time: {{ time }}</div>
    <button class="start-button" @click="startGame" v-if="!timerId">Start Game</button>
  </div>
</template>

<script>
export default {
  name: 'GameWidget',
  data() {
    return {
      moles: [],
      score: 0,
      time: 30,
      timerId: null
    }
  },
  mounted() {
    this.startGame()
  },
  methods: {
    startGame() {
      this.moles = Array(9).fill().map(() => ({ show: false }))
      this.score = 0
      this.time = 30
      this.timerId = setInterval(() => {
        this.time--
        if (this.time <= 0) {
          clearInterval(this.timerId)
          this.timerId = null
          alert(`Game Over! Your score: ${this.score}`)
        }
      }, 1000)
      this.showRandomMole()
    },
    showRandomMole() {
      const index = Math.floor(Math.random() * this.moles.length)
      this.moles[index].show = true
      setTimeout(() => {
        this.moles[index].show = false
        if (this.timerId) {
          this.showRandomMole()
        }
      }, Math.random() * 1500 + 500)
    },
    hitMole(index) {
      if (this.moles[index].show) {
        this.score++
        this.moles[index].show = false
      }
    }
  }
}
</script>

<style scoped>
.widget {
  margin: 20px;
  padding: 20px;
  border: 1px solid #ccc;
}

.game-container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 10px;
  width: 300px;
  height: 300px;
  margin: 0 auto;
}

.hole {
  position: relative;
  background-color: #92c9ff;
  border-radius: 50%;
  cursor: pointer;
}

.mole {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 80px;
  height: 80px;
  background-color: #754c24;
  border-radius: 50%;
}

.mole:hover {
  background-color: #ad762e;
}

.score {
  text-align: center;
  margin-top: 10px;
  font-weight: bold;
}

.time {
  text-align: center;
  margin-top: 10px;
  font-weight: bold;
}

.start-button {
  display: block;
  margin: 0 auto;
  margin-top: 20px;
}
</style>
