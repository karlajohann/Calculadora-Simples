<template>
 <div id="app">
  <calculadora></calculadora>
 </div>
</template>

<script>
import Calculadora from './components/Calculadora.vue'

export default {
  name: 'App',
  components: {
    Calculadora
  }
}
</script>

<style>
  body {
    background: #31475e;
  }

</style>
