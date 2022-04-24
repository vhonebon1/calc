<template lang='pug'>
  .the-calculator.text--ice
    .the-calculator__screen.bg--charcoal {{displayValue || 0}}
      .the-calculator__screen--clear.bg--ice.text--charcoal(@click='clear()') C
    .the-calculator__button.bg--stone(
      v-for='value in [7, 8, 9]' 
      @click='recordValue(value)'
    ) {{value}}
    .the-calculator__button.bg--goldfish(@click='operate("/")') /
    .the-calculator__button.bg--stone(
      v-for='value in [4, 5, 6]' 
      @click='recordValue(value)'
    ) {{value}}
    .the-calculator__button.bg--goldfish(@click='operate("*")') x
    .the-calculator__button.bg--stone(
      v-for='value in [1, 2, 3]' 
      @click='recordValue(value)'
    ) {{value}}
    .the-calculator__button.bg--goldfish(@click='operate("-")') -
    .the-calculator__button.bg--stone.br--bl(@click='recordValue(0)') 0
    .the-calculator__button.bg--goldfish(@click='decimal()') .
    .the-calculator__button.bg--goldfish(@click='evaluate()') =
    .the-calculator__button.bg--goldfish.br--br(@click='operate("+")') +
</template>

<script>
export default {
  name: 'TheCalculator',
  data() {
    return {
      inputValues: [],
      displayValue: '',
      errorMessage: 'ERROR'
    }
  },
  methods: {
    recordValue(value) {
      this.displayValue = `${this.displayValue}${value}`
    },
    decimal() {
      if (this.displayValue.indexOf('.') === -1) {
        this.recordValue('.')
      }
    },
    lastValue() {
      const regEx = /[+\-*/]/
      return this.displayValue.split(regEx).pop()
    },
    operate(operator) {
      this.inputValues.push(this.lastValue(), operator)
      this.recordValue(operator)
    },
    isValidEq() {
      const hasNumerals = this.inputValues.filter(value => !isNaN(parseFloat(value))).length
      const hasSingleNumeral = !isNaN(parseFloat(this.displayValue))
      return hasNumerals || hasSingleNumeral
    },
    evaluate() {
      if (this.isValidEq()) {
        this.inputValues.push(this.lastValue())
        const total = Function('"use strict";return (' + this.inputValues.join(' ') + ')')()
        if (total) {
          this.displayValue = total.toString()
          this.inputValues = []
        } else {
          this.displayError()
        }
      } else {
        this.displayError()
      }
    },
    displayError() {
      this.displayValue = this.errorMessage
    },
    clear() {
      this.displayValue = ''
      this.inputValues = []
    }
  }
}
</script>

<style lang='stylus' scoped>
@require '~/src/assets/styles'

.the-calculator
  --radius: 15px
  width: 400px
  display: grid
  grid-template-columns: repeat(4, 1fr)
  grid-template-rows: repeat(4, 100px)
  font-size: 1.5em

  &__screen
    position: relative
    grid-column: 1 / 5
    padding: 40px 8px
    border: 1px solid _COLOURS.charcoal
    border-bottom: none
    text-align: right
    font-size: 2em
    border-radius: var(--radius) var(--radius) 0 0

    &--clear
      --size: 26px
      height: var(--size)
      width: var(--size)
      position: absolute
      bottom: 5px
      border-radius: 50%
      font-size: 0.5em
      text-align: center
      cursor: pointer

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
