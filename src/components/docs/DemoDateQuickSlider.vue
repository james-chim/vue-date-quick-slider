<template>
  <div>
    <demo-day></demo-day>
    <demo-week></demo-week>
    <demo-month></demo-month>
    <demo-month-no-align></demo-month-no-align>
    <specification></specification>
  </div>
</template>

<script>
  import Specification from './Specification'
  import DemoDay from './DemoDay'
  import DemoWeek from './DemoWeek'
  import DemoMonth from './DemoMonth'
  import DemoMonthNoAlign from './DemoMonthNoAlign'

  export default {
    components: {
      Specification,
      DemoDay,
      DemoWeek,
      DemoMonth,
      DemoMonthNoAlign
    }
  }
</script>

<style>
</style>
