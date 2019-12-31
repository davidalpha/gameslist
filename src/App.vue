<template>
  <div id="app">
    <Games />
  </div>
</template>

<script>
import Games from './components/games.vue'

export default {
  name: 'app',
  components: {
    Games
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
