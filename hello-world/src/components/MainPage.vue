<template>
  <div :class="['main-page', { 'dark-mode': isDarkMode }]">

<div class="theme-switch-div">
    <label class="switch">
      <input type="checkbox" v-model="isDarkMode">
      <span class="slider round"></span>
    </label>
     <h4> {{ isDarkMode ? 'Theme 2' : 'Theme 1' }} </h4>
    </div>
   
    <div class="calculator">
      <div class="display">{{ currentOperand }}</div>
      <div class="buttons">
        <button class="sec-button" @click="clearDisplay">C</button>
        <button  @click="toggleSign" class="toggle-sign sec-button">+/-</button>
        <button class="sec-button" @click="calculatePercentage">%</button>
        <button class="special-buttons" @click="chooseOperation('/')">/</button>
        <button @click="appendNumber('7')">7</button>
        <button @click="appendNumber('8')">8</button>
        <button @click="appendNumber('9')">9</button>
        <button class="special-buttons" @click="chooseOperation('*')">x</button>
        <button @click="appendNumber('4')">4</button>
        <button @click="appendNumber('5')">5</button>
        <button @click="appendNumber('6')">6</button>
        <button class="special-buttons" @click="chooseOperation('-')">-</button>
        <button @click="appendNumber('1')">1</button>
        <button @click="appendNumber('2')">2</button>
        <button @click="appendNumber('3')">3</button>
        <button class="special-buttons" @click="chooseOperation('+')">+</button>

        <button class="zero-button" @click="appendNumber('0')">0</button>
        <button class="dot-button" @click="appendNumber('.')">.</button>
        <button class="special-buttons" @click="calculateResult">=</button>





      </div>
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
      hasDecimal: false,
      isDarkMode: false
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

      if (this.operator) {
        const prev = parseFloat(this.previousOperand);
        if (isNaN(prev)) {
          alert('Error: No base value for percentage calculation');
          return;
        }
        this.currentOperand = (curr / 100 * prev).toString();
      } else {
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
  width: 40%;

  border-radius: 5px;
  padding: 0;
  margin: 0;



}
h4{
  color: #ff9f0c;
  font-size: 1.5rem
}
.display {
  font-size: 34px;
  text-align: right;
  padding: 2rem 2rem 1.5rem 0;
  height: 1rem;
  background-color: rgba(50, 30, 0, 0.8);
}

.buttons {
  display: grid;
  grid-template-columns: repeat(4, 1fr);

}

button {
  width: 100%;
  padding: 10px;
  font-size: 16px;
  height: 5rem;
  border: 1px solid rgba(50, 30, 0, 0.8);
  cursor: pointer;
  background-color: rgba(132, 120, 102, 0.8);
  color: white;
}

.sec-button{
  background-color: rgba(91, 72, 51, 0.8);
}

button:hover {
background-color: rgba(173, 165, 153, 0.8);
}
.sec-button:hover{
  background-color: rgba(173, 165, 153, 0.8);
}


.main-page {
  text-align: center;
  padding: 50px;
  color: white;
  width: 80%;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}

.special-buttons {
  background-color: #ff9f0c;
}
.special-buttons:hover{
  background-color: #cc7f0a;
}
.zero-button {
  grid-column: span 2;
}
.dot-button {
  font-size: 26px;
}




.dark-mode h4 {
color: #cc0000;
}

.dark-mode button {
  border: 1px solid rgba(0, 0, 0, 0.5);
  background-color: rgba(102, 102, 102, 0.5) ;
 
}
.dark-mode button:hover{
  
  background-color: rgba(153, 153, 153, 0.5) ;
 
}
.dark-mode .sec-button:hover{
  
  background-color: rgba(153, 153, 153, 0.5) ;
 
}

.dark-mode .sec-button{
  background-color: rgba(51, 51, 51, 0.5);
}
.dark-mode .special-buttons:hover{
  background-color: #a30000;
}

.dark-mode .display {
  background-color: rgba(0, 0, 0, 0.5);
 
}

.dark-mode .special-buttons {
  background-color: #cc0000;
 
}

.theme-switch-div{
  display: flex;
  align-items: center;
  gap: 32px;
}

.switch {
  position: relative;
  display: inline-block;
  width: 60px;
  height: 34px;
  
}

.switch input {
  opacity: 0;
  width: 0;
  height: 0;
}

.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #ff9f0c;
  transition: .4s;
}

.slider:before {
  position: absolute;
  content: "";
  height: 26px;
  width: 26px;
  left: 4px;
  bottom: 4px;
  background-color: white;
  transition: .4s;
}

input:checked+.slider {
  background-color: #cc0000;
}

input:checked+.slider:before {
  transform: translateX(26px);
}

.slider.round {
  border-radius: 34px;
}

.slider.round:before {
  border-radius: 50%;
}
@media screen and (max-width: 800px) {
  .calculator{
   width: 80%;
  }
}

</style>
