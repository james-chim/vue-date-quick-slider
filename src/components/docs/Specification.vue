<template>
  <div class="mt-3">
    <h2>Props</h2>
    <b-table responsive striped small hover :items="properties"></b-table>
  </div>
</template>

<script>
  export default {
    name: 'FormDropdownSpecification',
    data () {
      return {
        properties: [
          {property: 'range-type', type: 'string', default_value: 'day', description: 'The view type of the component. Possible types includes "day", "week", "month", "year"'},
          {property: 'range-start-auto-align', type: 'boolean', default_value: 'true', description: 'To set if the component should always start from the beginning of the range. For example month view with this set as true will always start from the 1st.'},
          {property: 'start-date', type: 'JavaScript Date Object', default_value: '(current period)', description: 'Starting date of the range'},
          {property: 'end-date', type: 'JavaScript Date Object', default_value: '(current period)', description: 'Ending date of the range'},
          {property: 'display-format', type: 'string', default_value: 'D MMM', description: 'Accept all date format in Moment to be shown in slider'}
        ]
      }
    }
  }
</script>

<style>
</style>
