<template>
  <vueWeather></vueWeather>
</template>

<script>
import vueWeather from './components/vueWeather.vue'

export default {
  name: 'App',
  components: {
    vueWeather,
  }
}
</script>

<style>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color:rgb(160, 93, 223);
  margin-top: 60px;
}

.body {
  background-color: rgb(43, 43, 43);
}
</style>
