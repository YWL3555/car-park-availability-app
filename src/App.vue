<template>
  <div id="app">
    <Carparks />
  </div>
</template>

<script>
import Carparks from './components/Carparks.vue'

export default {
  name: 'app',
  components: {
    Carparks
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