<template lang='pug'>
  .base-calculator
    .base-calculator__screen {{current || 0}}
    .base-calculator__panel
      .base-calculator__panel--button(@click='display(7)') 7
      .base-calculator__panel--button(@click='display(8)') 8
      .base-calculator__panel--button(@click='display(9)') 9
      .base-calculator__panel--button /
      .base-calculator__panel--button(@click='display(4)') 4
      .base-calculator__panel--button(@click='display(5)') 5
      .base-calculator__panel--button(@click='display(6)') 6
      .base-calculator__panel--button x
      .base-calculator__panel--button(@click='display(1)') 1
      .base-calculator__panel--button(@click='display(2)') 2
      .base-calculator__panel--button(@click='display(3)') 3
      .base-calculator__panel--button -
      .base-calculator__panel--button(@click='display(0)') 0
      .base-calculator__panel--button .
      .base-calculator__panel--button =
      .base-calculator__panel--button +
</template>

<script>
export default {
  name: 'BaseCalculator',
  data() {
    return {
      input: [],
      current: '',
      evaluated: ''
    }
  },
  methods: {
    display(value) {
      this.current = `${this.current + value}`
    }
  }
}
</script>

<style lang='stylus' scoped>
.base-calculator
  width: 400px

  &__screen
    border: 1px solid grey
    padding: 15px 8px
    text-align: right

  &__panel
    display: grid
    justify-content: center
    align-items: center
    grid-template-columns: repeat(4, 100px)
    grid-template-rows: repeat(4, 100px)

    &--button
      text-align: center
      padding: 40px 0
      border: 1px solid grey

      &:hover
        cursor: pointer
</style>
