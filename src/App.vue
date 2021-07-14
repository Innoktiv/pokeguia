<template>
  <div id="app">
     <pokemon></pokemon>
  </div>
</template>

<script>
import Pokeguia from './components/Pokeguia.vue'

export default {
  name: 'App',
  components: {
    "pokemon":Pokeguia
  }
}
</script>

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
