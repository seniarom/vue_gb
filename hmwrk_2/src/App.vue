<template>

  <div class="app">

    <div class="form-label">
      <input type="number" v-for="op of 2" class="form-control mb-2" @click="chooseOperand(op)" v-model="operand[op]" />
      = {{ result }}
    </div>
    <div class="keyboard">
      <button class="btn" :class="{ active: currentOperation === item }" v-for="item of operations"
        @click="currentOperation = item">{{ item }}
      </button>
    </div>
    <div class="alert" v-show="error">Ошибка! {{ error }}</div>

    <div><input type="checkbox" id="checkbox" v-model="vKeyBoard">
      <label class="" for="checkbox">Отобразить экранную клавиатуру</label>
    </div>
    <div v-if="vKeyBoard" class="">
      <div>Выбранный операнд: {{ chosenOperand }}</div>
      <button class="btn" v-for="item of 9" @click="operand[chosenOperand] += item.toString()">{{
          item
      }}
      </button>
      <button class="btn" @click="operand[chosenOperand] = operand[chosenOperand].toString().slice(0, -1)">
        &#8592;
      </button>
    </div>

    <ul class="">
      <li class="" v-for="(log, index) in logs" v-bind:key="index">{{ log }}</li>
    </ul>

  </div>

</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      activeOperand: 1,
      vKeyBoard: false,
      operations: ['+', '-', '/', '*', 'x^y', '/целое'],
      currentOperation: "+",
      operand: {
        1: 0,
        2: 0
      },
      error: "",
      logs: {},
    }
  },
  computed: {
    result() {
      const result = this.calculate(this.currentOperation)
      return isNaN(result) ? "" : result
    }
  },
  methods: {
    enter() {
    },
    chooseOperand(num) {
      this.chosenOperand = num
    },
    calculate(operand) {
      this.error = ""
      switch (operand) {
        case "+":
          return this.sum()
        case "-":
          return this.minus()
        case "/":
          return this.divide()
        case "*":
          return this.mul()
        case "x^y":
          return this.pow()
        case "/целое":
          return this.divInt()
      }
      this.$set(this.logы, Date.now(), `${this.operand[1]}${operand}${this.operand[2]}=${this.result}`)
    },
    sum() {
      return Number(this.operand[1]) + Number(this.operand[2])
    },
    minus() {
      return this.operand[1] - this.operand[2]
    },
    divide() {
      if (this.operand[2] === 0) {
        this.error = "На ноль делить нельзя!"
        return
      }
      return this.operand[1] / this.operand[2]
    },
    mul() {
      return this.operand[1] * this.operand[2]
    },
    pow() {
      return Math.pow(this.operand[1], this.operand[2])
    },
    divInt() {
      if (this.operand[2] === 0) {
        this.error = "На ноль делить нельзя!"
        return
      }
      return Math.floor(this.operand[1] / this.operand[2])
    }
  }

}
</script>

<style lang="scss">
#app {
  font-family: 'Courier New', Courier, monospace;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.form-control {
  margin-left: 10px;
  border-radius: 5px;
}

.btn {
  background: turquoise;
  border-radius: 5px;
  padding: 10px;
  margin: 10px;
  font-family: 'Courier New', Courier, monospace;


  &:hover {
    cursor: pointer;
    background: palevioletred;
  }

  &:disabled {
    cursor: default;
  }
}
</style>
