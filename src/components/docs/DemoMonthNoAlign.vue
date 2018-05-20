<template>
  <div>
    <h2 class="my-3">Month View (No Auto Align)</h2>
    <date-quick-slider :start-date.sync="start" :end-date.sync="end" range-type="month" :range-start-auto-align="false"></date-quick-slider>
  </div>
</template>

<script>
  import DateQuickSlider from '@/components/lib/DateQuickSlider'

  export default {
    data () {
      return {
        start: undefined,
        end: undefined
      }
    },
    components: {
      DateQuickSlider
    }
  }
</script>

<style>
</style>
