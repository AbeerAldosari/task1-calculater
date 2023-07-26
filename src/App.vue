<template>
  <CalculatorAppComponent></CalculatorAppComponent>
</template>

<script>
import CalculatorAppComponent from './components/CalculatorAppComponent.vue'

export default {
  name: 'App',
  components: {
    CalculatorAppComponent
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
