<template>
  <div class="calculator">
    <div class="display">{{ currentOperand }}</div>
    <div class="buttons">
      <button @click="appendNumber('7')">7</button>
      <button @click="appendNumber('8')">8</button>
      <button @click="appendNumber('9')">9</button>
      <button @click="chooseOperation('/')">/</button>
      <button @click="appendNumber('4')">4</button>
      <button @click="appendNumber('5')">5</button>
      <button @click="appendNumber('6')">6</button>
      <button @click="chooseOperation('*')">*</button>
      <button @click="appendNumber('1')">1</button>
      <button @click="appendNumber('2')">2</button>
      <button @click="appendNumber('3')">3</button>
      <button @click="chooseOperation('-')">-</button>
      <button @click="appendNumber('0')">0</button>
      <button @click="clearDisplay">C</button>
      <button @click="calculateResult">=</button>
      <button @click="chooseOperation('+')">+</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      currentOperand: '',
      previousOperand: null,
      operator: null,
    };
  },
  methods: {
    appendNumber(number) {
      this.currentOperand += number;
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
  },
};
</script>

<style scoped>
.calculator {
  display: flex;
  flex-direction: column;
  width: 300px;
  margin: 0 auto;
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 5px;
}

.display {
  font-size: 24px;
  text-align: right;
  margin-bottom: 10px;
}

.buttons {
  display: flex;
  flex-wrap: wrap;
  gap: 5px;
}

button {
  width: calc(25% - 10px);
  padding: 10px;
  font-size: 16px;
  border: none;
  border-radius: 3px;
  cursor: pointer;
}

button:hover {
  background-color: #eee;
}
</style>
