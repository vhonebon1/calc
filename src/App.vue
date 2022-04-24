<template lang='pug'>
  #app
    the-calculator
</template>

<script>
import TheCalculator from './components/TheCalculator.vue'

export default {
  name: 'App',
  components: {
    TheCalculator
  }
}
</script>

<style lang='stylus'>
#app
  display: flex
  justify-content: center
</style>
