<template lang='pug'>
  .base-calculator
    .base-calculator__screen {{displayValue || 0}}
    .base-calculator__button(v-for='value in [7, 8, 9]' @click='display(value)') {{value}}
    .base-calculator__button(@click='operate("/")') /
    .base-calculator__button(v-for='value in [4, 5, 6]' @click='display(value)') {{value}}
    .base-calculator__button(@click='operate("*")') x
    .base-calculator__button(v-for='value in [1, 2, 3]' @click='display(value)') {{value}}
    .base-calculator__button(@click='operate("-")') -
    .base-calculator__button(@click='display(0)') 0
    .base-calculator__button(@click='decimal()') .
    .base-calculator__button(@click='evaluate()') =
    .base-calculator__button(@click='operate("+")') +
</template>

<script>
export default {
  name: 'BaseCalculator',
  data() {
    return {
      inputValues: [],
      displayValue: '',
      errorMessage: 'ERROR'
    }
  },
  methods: {
    display(value) {
      this.displayValue = `${this.displayValue}${value}`
    },
    decimal() {
      if (this.displayValue.indexOf('.') === -1) {
        this.display('.')
      }
    },
    lastValue() {
      const regEx = /[+\-*/]/
      return this.displayValue.split(regEx).pop()
    },
    operate(operator) {
      this.inputValues.push(this.lastValue(), operator)
      this.display(operator)
    },
    evaluate() {
      this.inputValues.push(this.lastValue())
      const total = eval(this.inputValues.join(' '))
      this.displayValue = total ? total.toString() : this.errorMessage
    }
  }
}
</script>

<style lang='stylus' scoped>
.base-calculator
  width: 400px
  display: grid
  grid-template-columns: repeat(4, 1fr)
  grid-template-rows: repeat(4, 100px)

  &__screen
    grid-column: 1 / 5
    padding: 40px 8px
    border: 1px solid grey
    border-bottom: none
    text-align: right

  &__button
    padding: 40px 0
    margin: 0 -1px -1px 0
    border: 1px solid grey
    text-align: center
    cursor: pointer
</style>
