<template>
  <div class="navbar d-flex justify-content-center">
    <v-menu href="/bmi">Kalkulator BMI</v-menu>
    <v-menu href="/exchange">Kursy Walut</v-menu>
  </div>

  <slot></slot>
</template>


<script>
import VMenu from '../components/menu.vue';
export default {
  components: {
    VMenu
  }
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
