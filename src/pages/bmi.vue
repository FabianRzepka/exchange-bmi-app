<template>
  <main-layout>
    <bmi msg="Kalkulator BMI"/>
  </main-layout>
</template>

<script>
import MainLayout from '../layouts/App.vue'
import bmi from '../components/bmi.vue'
export default {
  components: {
    MainLayout,
    bmi
  }
}
</script>