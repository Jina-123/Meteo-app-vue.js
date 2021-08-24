<template>
  <div id="app"> 
    <meteo></meteo>
  </div>
</template>

<script>
import Meteo from './components/Meteo.vue'

export default {
  name: 'App',
  components: {
    'meteo': Meteo
  }
}
</script>

<style>
body {
  background-image: url('./assets/fondecran.jpg');
  background-repeat: no-repeat;
  background-attachment: fixed;
  background-size: 100% 100%;
}
</style>
