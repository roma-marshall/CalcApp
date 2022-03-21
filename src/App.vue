<template>
  <div>
    <CalculatorMain

    />
  </div>
</template>

<script>
import CalculatorMain from '@/components/CalculatorMain.vue'

export default {
  name: 'App',
  components: {
    CalculatorMain
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
