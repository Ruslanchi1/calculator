<template>
  <div class="container">
    <div class="calc">
      <div class="calc__screen">
        <input v-model="calculatorValue" type="text" class="screen"/>
      </div>
      <div class="calc__but">
        <div class="buttons">
          <button 
            class="btn" 
            :class="{'zero': '0'.includes(n)}"
            v-for="n in calculatorElements" 
            :key="n"
            @click="action(n)"
          >
            {{ n }}
          </button>
          <!-- <div class="btn C"><button>C</button></div>
                <div class="btn +/-"> <button>+/-</button></div>
                <div class="btn %"> <button> %</button></div>
                <div class="btn /"> <button>/</button></div>
                <div class="btn 7"> <button>7</button></div>
                <div class="btn 8"> <button>8</button></div>
                <div class="btn 9"> <button>9</button></div>
                <div class="btn X"> <button>X</button></div>
                <div class="btn 4"> <button>4</button></div>
                <div class="btn 5"> <button>5</button></div>
                <div class="btn 6"> <button>6</button></div>
                <div class="btn -"> <button>-</button></div>
                <div class="btn 1"> <button>1</button></div>
                <div class="btn 2"> <button>2</button></div>
                <div class="btn 3"> <button>3</button></div>
                <div class="btn +"> <button>+</button></div>
                <div class="btn zero"> <button>0</button></div>
                <div class="btn ,"> <button>,</button></div>
                <div class="btn ="> <button>=</button></div> -->
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      calculatorValue: '',
      calculatorElements: [
        "C",
        "+/-",
        "%",
        "/",
        "7",
        "8",
        "9",
        "*",
        "4",
        "5",
        "6",
        "-",
        "1",
        "2",
        "3",
        "+",
        "0",
        ",",
        "=",
      ],
      operator: null,
      previousCalculatorValue: ''
    }
  },
  methods: {
    action(n) {
      if (!isNaN(n) || n === ',') {
        this.calculatorValue += n + ''
      }

      if (n === 'C') {
        this.calculatorValue = ''
      }

      if (n === '%') {
        this.calculatorValue = this.calculatorValue / 100 + ''
        console.log(this.calculatorValue)
      }

      if (n === '+/-') {
        this.calculatorValue = this.calculatorValue * -1 + ''
      }

      if ( ['/','*','-','+'].includes(n)) {
        this.operator = n
        this.previousCalculatorValue = this.calculatorValue
        this.calculatorValue = ''
      }

      if (n === '=') {
        this.calculatorValue = eval(this.previousCalculatorValue + this.operator + this.calculatorValue)
        
        this.previousCalculatorValue = '';
        this.operator = null;
      }
    }
  }
};
</script>

<style>
</style>
