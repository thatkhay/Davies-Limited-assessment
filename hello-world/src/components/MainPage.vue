<template>
  <ThemeSwitch />
  
  <div class="calculator">
    <div class="display">{{ currentOperand }}</div>
    <div class="buttons">
      <button @click="clearDisplay">C</button>
      <button @click="toggleSign" class="toggle-sign">+/-</button>
      <button @click="calculatePercentage">%</button>
      <button @click="chooseOperation('/')">/</button>
      <button @click="appendNumber('7')">7</button>
      <button @click="appendNumber('8')">8</button>
      <button @click="appendNumber('9')">9</button>
       <button @click="chooseOperation('*')">x</button>
      <button @click="appendNumber('4')">4</button>
      <button @click="appendNumber('5')">5</button>
      <button @click="appendNumber('6')">6</button>
       <button @click="chooseOperation('-')">-</button>
      <button @click="appendNumber('1')">1</button>
      <button @click="appendNumber('2')">2</button>
      <button @click="appendNumber('3')">3</button>
     <button @click="chooseOperation('+')">+</button>
      <button @click="appendNumber('0')">0</button>
        <button @click="appendNumber('.')">.</button>
      <button @click="calculateResult">=</button>
     


    </div>
  </div>
</template>

<script>
import ThemeSwitch from './ThemeSwitch.vue';

export default {
  components: {
    ThemeSwitch, 
  },
  data() {
    return {
      currentOperand: '',
      previousOperand: null,
      operator: null,
      hasDecimal: false,
    };
  },
  methods: {
    appendNumber(number) {
    if (number === '.' && this.hasDecimal) return; 
    this.currentOperand += number;
    this.hasDecimal = this.currentOperand.includes('.'); 
  },
    chooseOperation(op) {
      this.operator = op;
      this.previousOperand = this.currentOperand;
      this.currentOperand = '';
    },
    clearDisplay() {
      this.currentOperand = '';
      this.previousOperand = null;
      this.operator = null;
    },
    calculateResult() {
      let result;
      const prev = parseFloat(this.previousOperand);
      const curr = parseFloat(this.currentOperand);
      if (isNaN(prev) || isNaN(curr)) return;
      switch (this.operator) {
        case '+':
          result = prev + curr;
          break;
        case '-':
          result = prev - curr;
          break;
        case '*':
          result = prev * curr;
          break;
        case '/':
          if (curr === 0) {
            alert('Error: Division by zero');
            return;
          }
          result = prev / curr;
          break;
        default:
          break;
      }
      this.currentOperand = result.toString();
      this.previousOperand = null;
      this.operator = null;
    },
    toggleSign() {
      if (this.currentOperand !== '') {
        this.currentOperand = parseFloat(this.currentOperand) * -1;
        this.currentOperand = this.currentOperand.toString();
      }
    },
  calculatePercentage() {
  const curr = parseFloat(this.currentOperand);
  if (isNaN(curr)) return;

  if (this.operator) { // Percentage of previous operand
    const prev = parseFloat(this.previousOperand);
    if (isNaN(prev)) {
      alert('Error: No base value for percentage calculation');
      return;
    }
    this.currentOperand = (curr / 100 * prev).toString();
  } else { // Percentage itself (10% key)
    this.currentOperand = (curr / 100).toString();
  }
},



 
  },
};
</script>

<style scoped>
.calculator {
  display: flex;
  flex-direction: column;
  width: 80%;
  border: 1px solid #ddd;
  border-radius: 5px;
  padding: 0;
  margin: 0;
}

.display {
  font-size: 24px;
  text-align: right;
  padding: 2rem 2rem 1rem 0;
  height: 1rem;
}

.buttons {
  display: grid;
  grid-template-columns: repeat(4, 1fr);

}

button {
  width: 100%;
  padding: 10px;
  font-size: 16px;

  border: 1px solid black;
  cursor: pointer;
}


button:hover {
  background-color: #eee;
}
</style>
