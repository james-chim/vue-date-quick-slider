<template>
  <div id="app">
    <day-slider :start-date.sync="start" :end-date.sync="end"></day-slider>
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
      start: undefined,
      end: new Date(500000)
    }
  }
}
</script>

<style>
</style>
