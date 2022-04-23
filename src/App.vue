<template lang='pug'>
  #app
    base-calculator
</template>

<script>
import BaseCalculator from './components/BaseCalculator.vue'

export default {
  name: 'App',
  components: {
    BaseCalculator
  }
}
</script>

<style lang='stylus'>
#app
  display: flex
  justify-content: center
</style>
