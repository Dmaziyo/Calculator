<template>
  <div class="calculator">
    <div class="display">{{ current || '0' }}</div>
    <div @click="clear" class="m_btn operator">C</div>
    <div @click="sign" class="m_btn operator">+/-</div>
    <div @click="percent" class="m_btn operator">%</div>
    <div @click="divide" class="m_btn operator">÷</div>
    <div @click="append('7')" class="m_btn">7</div>
    <div @click="append('8')" class="m_btn">8</div>
    <div @click="append('9')" class="m_btn">9</div>
    <div @click="times" class="m_btn operator">X</div>
    <div @click="append('4')" class="m_btn">4</div>
    <div @click="append('5')" class="m_btn">5</div>
    <div @click="append('6')" class="m_btn">6</div>
    <div @click="divide" class="m_btn operator">-</div>
    <div @click="append('1')" class="m_btn">1</div>
    <div @click="append('2')" class="m_btn">2</div>
    <div @click="append('3')" class="m_btn">3</div>
    <div @click="add" class="m_btn operator">+</div>
    <div @click="append('0')" class="m_btn zero">0</div>
    <div @click="dot" class="m_btn operator">.</div>
    <div @click="equal" class="m_btn operator">=</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      current: '',
      operatorClicked: false,
      previous: undefined,
      operator: null
    }
  },
  methods: {
    append(number) {
      if (this.operatorClicked) {
        this.current = ''
        this.operatorClicked = false
      }
      this.current += number
    },
    clear() {
      this.current = ''
    },
    sign() {
      this.current =
        this.current.charAt(0) === '-'
          ? this.current.slice(0, 1)
          : `-${this.current}`
    },
    percent() {
      this.current = `${parseFloat(this.current) / 100}`
    },
    dot() {
      if (this.current.indexOf('.') === -1) {
        this.append('.')
      }
    },
    setPrevious() {
      this.previous = this.current
      this.operatorClicked = true
    },
    add() {
      this.operator = (a, b) => a + b
      this.setPrevious()
    },
    minus() {
      this.operator = (a, b) => a - b
      this.setPrevious()
    },
    times() {
      this.operator = (a, b) => a * b
      this.setPrevious()
    },
    divide() {
      this.operator = (a, b) => a / b
      this.setPrevious()
    },
    equal() {
      if (this.previous == null) {
        this.operatorClicked = true
        return this.current
      }
      this.current = `${this.operator(
        parseFloat(this.previous),
        parseFloat(this.current)
      )}`
      this.previous = null
      this.operatorClicked = true
    }
  }
}
</script>

<style scoped>
.m_btn {
  background-color: white;
  border: 1px solid #bfbfbf;
  font-size: 30px;
}
.calculator {
  background-color: #bfbfbf;
  margin: 0 auto;
  width: 400px;
  font-size: 40px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
}
/* 显示计算结果 */
.display {
  grid-column: 1/5;
}
/* 设置0的大小 */
.zero {
  grid-column: 1/3;
}

.m_btn.operator {
  background-color: #d8d8d8;
}
</style>