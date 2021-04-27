<template>
  <div class="hello">
    <input v-model.number="operand1"/>
    <input v-model.number="operand2"/>
    = {{ result }}
    <div class="buttons">
      <button @click="calculate('+')">+</button>
      <button @click="calculate('-')">-</button>
      <button @click="calculate('/')">/</button>
      <button @click="calculate('*')">*</button>
      <button @click="calculate('pow')">pow</button>
      <button @click="calculate('trunc')">trunc</button>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      operand1: 0,
      operand2: 0,
      result: 0
    }
  },
  methods: {
    // calculate2 (arg) {
    //   switch (arg) {
    //     case 'sum':
    //       this.result = this.operand1 + this.operand2
    //       break
    //     case 'sub':
    //       this.result = this.operand1 - this.operand2
    //       break
    //     case 'div':
    //       this.result = this.operand1 / this.operand2
    //       break
    //     case 'mul':
    //       this.result = this.operand1 * this.operand2
    //       break
    //     default:
    //       alert('Где то ошибка')
    //       break
    //   }
    // },
    calculate (arg) {
      if (arg === 'pow') {
        this.result = Math.pow(this.operand1, this.operand2)
      } else if (arg === 'trunc') {
        this.result = Math.trunc(this.operand1 / this.operand2)
      } else {
        /* eslint-disable-next-line */
        this.result = eval(`${this.operand1} ${arg} ${this.operand2}`)
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
.hello {
  .buttons {
    margin-top: 10px;
    height: 20px;
    button {
      margin-right: 10px;
    }
  }
}
</style>
