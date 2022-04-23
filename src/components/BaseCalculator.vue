<template lang='pug'>
  .base-calculator.text--ice
    .base-calculator__screen.bg--charcoal {{displayValue || 0}}
    .base-calculator__button.bg--stone(
      v-for='value in [7, 8, 9]' 
      @click='display(value)'
    ) {{value}}
    .base-calculator__button.bg--goldfish(@click='operate("/")') /
    .base-calculator__button.bg--stone(
      v-for='value in [4, 5, 6]' 
      @click='display(value)'
    ) {{value}}
    .base-calculator__button.bg--goldfish(@click='operate("*")') x
    .base-calculator__button.bg--stone(
      v-for='value in [1, 2, 3]' 
      @click='display(value)'
    ) {{value}}
    .base-calculator__button.bg--goldfish(@click='operate("-")') -
    .base-calculator__button.bg--stone.br--bl(@click='display(0)') 0
    .base-calculator__button.bg--goldfish(@click='decimal()') .
    .base-calculator__button.bg--goldfish(@click='evaluate()') =
    .base-calculator__button.bg--goldfish.br--br(@click='operate("+")') +
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
@require '~/src/assets/styles'

.base-calculator
  --radius: 15px
  width: 400px
  display: grid
  grid-template-columns: repeat(4, 1fr)
  grid-template-rows: repeat(4, 100px)
  font-size: 1.5em

  &__screen
    grid-column: 1 / 5
    padding: 40px 8px
    border: 1px solid _COLOURS.charcoal
    border-bottom: none
    text-align: right
    font-size: 2em
    border-radius: var(--radius) var(--radius) 0 0

  &__button
    padding: 40px 0
    margin: 0 -1px -1px 0
    border: 1px solid _COLOURS.charcoal
    text-align: center
    cursor: pointer

  .br
    &--bl
      border-bottom-left-radius: var(--radius)

    &--br
      border-bottom-right-radius: var(--radius)
</style>
