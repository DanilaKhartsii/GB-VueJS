<template>
  <div class="hello">
    <input ref="op1" v-model.number="operand1"/>
    <input ref="op2" v-model.number="operand2"/>
    = {{ result }}
    <div class="buttons">
      <button
        v-for="(op, index) in operationsBtn"
        :key="`op-${index}`"
        @click="calculate(op.operation)"
      > {{ op.value }}
      </button>
    </div>
    <div class="desktop-keyboard">
      <input id="check" v-model="checked" type="checkbox">
      <label for="check">Отобразить экранную клавиатуру</label>
      <div v-if="checked" class="keyboard">
        <div class="numbers-btns">
          <button v-for="i of numbers" :key="i" @click="addValue(i)">{{ i }}</button>
        </div>
        <div class="delete-btns">
          <button class="delete" @click="clearOperandLastDigit">C</button>
          <button class="delete" @click="clearAll">delete all</button>
        </div>
        <br>
        <input id="one" v-model="operandValue" type="radio" value="Operand1">
        <label for="one">Операнд 1</label>
        <input id="two" v-model="operandValue" type="radio" value="Operand2">
        <label for="two">Операнд 2</label>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      operand1: [],
      operand2: [],
      result: 0,
      checked: false,
      operandValue: '',
      operationsBtn: [
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
      ],
      numbers: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
    }
  },
  watch: {
    operandValue (newValue) {
      if (newValue === 'Operand1') {
        // фокусим первое поле
        this.$refs.op1.focus()
      } else {
        // фокусим второе поле
        this.$refs.op2.focus()
      }
    }
  },
  methods: {
    calculate (arg) {
      const {
        operand1,
        operand2
      } = this
      const mathOperations = {
        sum: () => +operand1 + +operand2,
        sub: () => operand1 - operand2,
        div: () => Number((operand1 / operand2).toFixed(2)),
        mul: () => operand1 * operand2,
        pow: () => Math.pow(operand1, operand2),
        trunc: () => Math.trunc(operand1 / operand2)
      }
      this.result = mathOperations[arg]()
    },
    addValue (arg) {
      if (this.operandValue === 'Operand1') {
        this.operand1 += arg
      }
      if (this.operandValue === 'Operand2') {
        this.operand2 += arg
      }
    },
    clearOperandLastDigit () {
      if (this.operandValue === 'Operand1') {
        this.operand1 = this.operand1.slice(0, -1)
      }
      if (this.operandValue === 'Operand2') {
        this.operand2 = this.operand2.slice(0, -1)
      }
    },
    clearAll () {
      this.operand1 = []
      this.operand2 = []
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

  .desktop-keyboard {
    margin-top: 20px;
    .numbers-btns {
      margin-top: 20px;
      button {
        margin-right: 5px;
      }
    }
    .delete-btns {
      margin-top: 20px;
      button {
        margin-right: 5px;
      }
    }
  }
}
</style>
