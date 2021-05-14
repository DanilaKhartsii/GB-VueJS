<template>
  <div class="hello">
    <input v-model.number="operand1"/>
    <input v-model.number="operand2"/>
    = {{ result }}
    <div class="buttons">
      <button
        v-for="btn in buttons"
        :key="btn"
        @click="calculate(btn.operation)"
      > {{ btn.value }} </button>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      operand1: 0,
      operand2: 0,
      result: 0,
      buttons: [
        {
          operation: 'sum',
          value: '+'
        },
        {
          operation: 'sub',
          value: '-'
        },
        {
          operation: 'div',
          value: '/'
        },
        {
          operation: 'mul',
          value: '*'
        },
        {
          operation: 'pow',
          value: 'pow'
        },
        {
          operation: 'trunc',
          value: 'trunc'
        }
      ]
    }
  },
  methods: {
    calculate (arg) {
      const {
        operand1,
        operand2
      } = this
      const mathOperations = {
        sum: () => operand1 + operand2,
        sub: () => operand1 - operand2,
        div: () => (operand1 / operand2).toFixed(2),
        mul: () => operand1 * operand2,
        pow: () => Math.pow(operand1, operand2),
        trunc: () => Math.trunc(operand1 / operand2)
      }
      this.result = mathOperations[arg]()
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
