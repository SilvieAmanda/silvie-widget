<template>
  <div class="hello">
    <h1>{{ greeting }}</h1>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data() {
    return {
      greeting: 'Hello, World!'
    }
  }
}
</script>

<style scoped>
h1 {
  color: #42b983;
}
</style>
