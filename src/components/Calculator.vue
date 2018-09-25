<script>
export default {
  data(){
    return {
      calculator: {
        previous: null,
        current: '',
        operator: null,
        operatorClicked: false
      }
    }
  },
  methods: {
    clearAll() {
      this.calculator.current = ''
    },
    sign() {
      this.calculator.current = this.calculator.current.charAt(0) === '-' ?
      this.calculator.current.slice(1) : `-${this.calculator.current}`
    },
    percent() {
      this.calculator.current = `${parseFloat(this.calculator.current) / 100}`
    },
    append(number) {
      if(this.calculator.operatorClicked) {
        this.calculator.current = ''
        this.calculator.operatorClicked = false
      }
      this.calculator.current = `${this.calculator.current}${number}`
    },
    dot() {
      if (this.calculator.current.indexOf('.') === -1)
        this.append('.')
    },
    setPrevious() {
      this.calculator.previous = this.calculator.current
      this.calculator.operatorClicked = true;
    },
    divide() {
      this.calculator.operator = (a, b) => a / b
      this.setPrevious()
    },
    times() {
      this.calculator.operator = (a, b) => a * b
      this.setPrevious()
    },
    minus() {
      this.calculator.operator = (a, b) => a - b
      this.setPrevious()
    },
    add() {
      this.calculator.operator = (a, b) => a + b
      this.setPrevious()
    },
    equal() {
      this.calculator.current = this.calculator.operator(
        parseFloat(this.calculator.previous),
        parseFloat(this.calculator.current)
      )
      this.calculator.previous = null
    },
    del() {
      if(this.calculator.current)
        this.calculator.current = this.calculator.current.slice(0, -1)
    },
    sqrt() {
      if(parseFloat(this.calculator.current) >= 0)
        this.calculator.current = Math.sqrt(parseFloat(this.calculator.current))
    },
    pow() {
      this.calculator.current = Math.pow(parseFloat(this.calculator.current),2)
    },
    inverse() {
      if(parseFloat(this.calculator.current) > 0)
        this.calculator.current = 1 / parseFloat(this.calculator.current)
    }
  }
}
</script>

<template>
  <div class="container">
    <div class="calculator">
      <div class="display">{{ calculator.current || '0' }}</div>
      <div @click="percent" class="btn operator">%</div>
      <div @click="sqrt" class="btn operator">&#x221a;</div>
      <div @click="pow" class="btn operator">x²</div>
      <div @click="inverse" class="btn operator">1/x</div>
      <div @click="clearAll" class="btn operator2 c">C</div>
      <div @click="del" class="btn operator2">🔙</div>
      <div @click="divide" class="btn operator2">÷</div>
      <div @click="append('7')" class="btn">7</div>
      <div @click="append('8')" class="btn">8</div>
      <div @click="append('9')" class="btn">9</div>
      <div @click="times" class="btn operator2">x</div>
      <div @click="append('4')" class="btn">4</div>
      <div @click="append('5')" class="btn">5</div>
      <div @click="append('6')" class="btn">6</div>
      <div @click="minus" class="btn operator2">-</div>
      <div @click="append('1')" class="btn">1</div>
      <div @click="append('2')" class="btn">2</div>
      <div @click="append('3')" class="btn">3</div>
      <div @click="add" class="btn operator2">+</div>
      <div @click="sign" class="btn">±</div>
      <div @click="append('0')" class="btn">0</div>
      <div @click="dot" class="btn">.</div>
      <div @click="equal" class="btn operator2">=</div>
    </div>
  </div>
</template>

<style scoped>
* { font-size: 25px }

.calculator {
  margin: 0 auto;
  width: 300px;
  height: 400px;
  text-align: center;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(30px, auto);
}

.display {
  padding: 2px;
  grid-column:  1 / 5;
  display: flex;
  justify-content: flex-end;
  align-items: center;
  background-color: #333;
  color: #fff;
}

.c {
  grid-column:  1 / 3;
}

.btn {
  background-color: #f2f2f2;
  border: 1px solid #999;
  display: flex;
  justify-content: center;
  align-items: center;
}

.operator { background-color: chocolate }
.operator2 { background-color: coral }

</style>


