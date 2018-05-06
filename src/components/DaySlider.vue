<template>
  <div>
    <back-svg class="slider-control"></back-svg>
    <div class="slider-date"></div>
    <forward-svg class="slider-control"></forward-svg>
  </div>
</template>

<script>
import backSvg from '../assets/ion-ios-back.svg'
import forwardSvg from '../assets/ion-ios-forward.svg'

import moment from 'moment'

export default {
  name: 'DaySlider',
  components: {
    backSvg,
    forwardSvg
  },
  data () {
    return {}
  },
  props: {
    startDate: {
      default: () => {
        return moment().startOf('day')
      },
      validator: (value) => {
        return moment(value)._isValid
      }
    },
    endDate: {
      default: () => {
        return moment().endOf('day')
      },
      validator: (value) => {
        return moment(value)._isValid
      }
    },
    startDateLimit: {
      validator: (value) => {
        return moment(value)._isValid
      }
    },
    endDateLimit: {
      validator: (value) => {
        return moment(value)._isValid
      }
    }
  },
  created () {
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
  .slider-date {
    display: inline-block;
  }
  .slider-control {
    width: 50px;
    transition: all 300ms ease;
    &:hover {
      fill: red;
    }
  }
</style>
