<template>
  <div id="app">
    <day-slider :start-date.sync="start" :end-date.sync="end" range-type="week"></day-slider>
  </div>
</template>

<script>
import DaySlider from './components/DateQuickSlider'

export default {
  name: 'app',
  components: {
    DaySlider
  },
  data () {
    return {
      start: undefined,
      end: undefined
    }
  }
}
</script>

<style>
</style>
