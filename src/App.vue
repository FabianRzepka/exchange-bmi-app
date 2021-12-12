<template>
<!--  <img alt="Vue logo" src="./assets/logo.png">-->
  <bmi msg="Kalkulator BMI"/>
</template>

<script>
import bmi from './components/bmi.vue'

export default {
  name: 'App',
  components: {
    bmi
  },
}
</script>

<style>
#app {
  font-family: 'Bai Jamjuree', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity .5s ease;
}

.fade-enter-from, .fade-leave-to {
  opacity: 0;
}
</style>
