<template>
  <div class="app">
    <CalculatorMain/>
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
html {
  font-size: 62.5%;
  box-sizing: border-box;
}

*, *::before, *::after {
  margin: 0;
  padding: 0;
  box-sizing: inherit;
}

.app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin: 10px auto;
  border: 1px solid #ccc;
  background: #283637;
  border-radius: 30px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 370px;
}
</style>
