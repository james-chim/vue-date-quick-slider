<template>
  <div>
    <back-svg class="slider-control"></back-svg>
    <div class="slider-date">{{startDate}}</div>
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
    rangeType: {
      type: String,
      default: () => {
        // changing this also requires you to change the default function of startDate
        return 'day'
      },
      validator: (value) => {
        // The value must match one of these strings
        return ['day', 'week', 'month', 'year'].indexOf(value) !== -1
      }
    },
    rangeStartAutoAlign: {
      type: Boolean,
      // changing this also requires you to change the default function of startDate
      default: () => true
    },
    startDate: {
      default: () => {
        // checking for undefined since those props are dependent on this generation
        if (typeof this.rangeStartAutoAlign === 'undefined' || this.rangeStartAutoAlign) {
          var tempRangeType = this.rangeType
          if (typeof tempRangeType === 'undefined') {
            tempRangeType = 'day'
          }
          return moment().startOf(tempRangeType)
        }
        return moment().startOf('day')
      },
      validator: (value) => {
        return moment(value)._isValid
      }
    },
    endDate: {
      default: () => {
        return moment().endOf(this.rangeType)
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
  watch: {
    startDate (newVal) {
      console.log(newVal)
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
