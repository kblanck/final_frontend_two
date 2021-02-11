<template>
  <div id="app">
    <Glasses/>
    <AddGlasses/>
  </div>
</template>

<script>
import Glasses from './components/Glasses.vue'
import AddGlasses from './components/AddGlasses.vue'
export default {
  name: 'App',
  components: {
    Glasses,
    AddGlasses
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
  /* margin-top: 1.5em; */
}
</style>