<template>
  <div id="app">
    <day-slider :start-date="random"></day-slider>
  </div>
</template>

<script>
import DaySlider from './components/DaySlider'

export default {
  name: 'app',
  components: {
    DaySlider
  },
  data () {
    return {
      random: new Date()
    }
  }
}
</script>

<style>
</style>
