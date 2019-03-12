<template>
  <div id="app">
    <img src="./assets/logo.png">
    <ChooseRestaurants/>
  </div>
</template>

<script>
import ChooseRestaurants from './components/ChooseRestaurants'

export default {
  name: 'App',
  components: {
     ChooseRestaurants
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
