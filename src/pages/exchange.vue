<template>
  <main-layout>
    <exchange msg="Kurs walut"/>
  </main-layout>
</template>

<script>
import MainLayout from '../layouts/App.vue';
import exchange from '../components/exchange.vue';

export default {
  components: {
    MainLayout,
    exchange
  }
}
</script>