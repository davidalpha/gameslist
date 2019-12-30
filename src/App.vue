<template>
  <div id="app">
    <games />
  </div>
</template>

<script>
import games from './components/games.vue'

export default {
  name: 'app',
  components: {
    games
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
