<template>
  <div id="app">
    <div class="input-forms">
      <input class="form-control" v-model="operand1" />
      <input class="form-control" v-model="operand2" />
      = {{ result }}
    </div>
    <div class="keyboard">
      <button class="btn" @click="result = Number(operand1) + Number(operand2)">+</button>
      <button class="btn" @click="result = operand1 - operand2">-</button>
      <button class="btn" @click="result = operand1 / operand2">/</button>
      <button class="btn" @click="result = operand1 * operand2">*</button>
      <button class="btn" @click="result = Math.pow(operand1, operand2)">x<sup>y</sup></button>
      <button class="btn" @click="result = Math.floor(operand1 / operand2)">/(целое)</button>
    </div>
  </div>
</template>

<script>


export default {
  name: 'App',
  data() {
    return {
      operand1: 0,
      operand2: 0,
      result: 0
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
