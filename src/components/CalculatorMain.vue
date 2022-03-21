<template>
  <div class="app">
    <div>
      <small v-if="selectedOperation">{{ prevNum }} {{ selectedOperation }} {{ currentNum }}</small>
      <div>
        <h1>{{ currentNum }}</h1>
      </div>
    </div>
    <div>
      <button @click="pressed('c')">c</button>
      <button @click="pressed('()')">()</button>
      <button @click="pressed('%')">%</button>
      <button @click="pressed('/')">/</button>
      <button @click="pressed('7')">7</button>
      <button @click="pressed('8')">8</button>
      <button @click="pressed('9')">9</button>
      <button @click="pressed('*')">*</button>
      <button @click="pressed('4')">4</button>
      <button @click="pressed('5')">5</button>
      <button @click="pressed('6')">6</button>
      <button @click="pressed('-')">-</button>
      <button @click="pressed('1')">1</button>
      <button @click="pressed('2')">2</button>
      <button @click="pressed('3')">3</button>
      <button @click="pressed('+')">+</button>
      <button @click="negateValue">+/-</button>
      <button @click="pressed('0')">0</button>
      <button @click="pressed('.')">.</button>
      <button @click="pressed('=')">=</button>
    </div>
  </div>
</template>

<script>
import {ref, onMounted} from "vue";

export default {
  setup() {
    const operations = ['+', '-', '*', '/', '%', '()'];
    const numbers = ['1', '2', '3', '4', '5', '6', '7', '8', '9', '0', '.'];
    const currentNum = ref('');
    const prevNum = ref('');
    const selectedOperation = ref('');
    const total = ref('');
    const pressed = (value) => {
      if (value === '=' || value === 'Enter')
        calculate();
      else if (value === '%') percentage();
      else if (value === 'c') clear();
      else if (value === 'Backspace') deleteValue();
      else if (operations.includes(value)) applyOperation(value);
      else if (numbers.includes(value)) appendNumber(value);
    }
    const appendNumber = (value) => {
      currentNum.value = currentNum.value + value;
    }
    const applyOperation = (value) => {
      calculate();
      prevNum.value = currentNum.value;
      currentNum.value = '';
      selectedOperation.value = value;
    }
    const calculate = () => {
      if (selectedOperation.value === '*') multiply();
      if (selectedOperation.value === '()') multiply();
      else if (selectedOperation.value === '/') divide();
      else if (selectedOperation.value === '%') percentage();
      else if (selectedOperation.value === '-') subtract();
      else if (selectedOperation.value === '+') sum();
      prevNum.value = '';
      selectedOperation.value = '';
    }
    const multiply = () => {
      currentNum.value = prevNum.value * currentNum.value;
      total.value = currentNum.value;
    }
    const divide = () => {
      currentNum.value = prevNum.value / currentNum.value;
      total.value = currentNum.value;
    }
    const percentage = () => {
      currentNum.value = currentNum.value / 100;
      total.value = currentNum.value;
    }
    const subtract = () => {
      currentNum.value = prevNum.value - currentNum.value;
      total.value = currentNum.value;
    }
    const sum = () => {
      currentNum.value = +prevNum.value + +currentNum.value;
      total.value = currentNum.value;
    }
    const clear = () => {
      currentNum.value = ''
      prevNum.value = ''
      selectedOperation.value = ''
      currentNum.value = ''
    }
    const deleteValue = () => {
      if (currentNum.value.length !== 0 && currentNum.value !== '0') {
        currentNum.value = currentNum.value.slice(0, -1)
      }
    }
    const negateValue = () => {
      if (currentNum.value === '0')
        return currentNum.value = '-0';
      if (currentNum.value === '-')
        return currentNum.value = '0';
      if (currentNum.value === '0.')
        return currentNum.value = `-${currentNum.value}`;
      if (currentNum.value === '-0.')
        return currentNum.value = '0.';
      currentNum.value = `${currentNum.value * -1}`
    }
    const handleKeydown = (e) => {
      pressed(e.key);
    }
    onMounted(() => window.addEventListener('keydown', handleKeydown));
    return {
      currentNum,
      pressed,
      selectedOperation,
      prevNum,
      negateValue,
      deleteValue,
      total,
    };
  }
}
</script>

<style scoped>

</style>