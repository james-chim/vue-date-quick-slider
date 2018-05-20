<template>
  <div>
    <h2 class="my-3">Day View</h2>
    <date-quick-slider :start-date.sync="start" :end-date.sync="end" range-type="day"></date-quick-slider>
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
