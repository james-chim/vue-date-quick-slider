<template>
  <div>
    <div @click="previousRange()">
      <back-svg class="slider-control"></back-svg>
    </div>
    <div class="slider-date">{{startDate}} - {{endDate}}</div>
    <div @click="nextRange()">
      <forward-svg class="slider-control"></forward-svg>
    </div>
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
    return {
      startDateLocal: undefined,
      endDateLocal: undefined
    }
  },
  props: {
    rangeType: {
      type: String,
      default: () => {
        return 'day'
      },
      validator: (value) => {
        // The value must match one of these strings
        return ['day', 'week', 'month', 'year'].indexOf(value) !== -1
      }
    },
    rangeStartAutoAlign: {
      type: Boolean,
      default: () => true
    },
    startDate: {
      validator: (value) => {
        return moment(value)._isValid
      }
    },
    endDate: {
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
    startDateLocal: {
      handler (newValue) {
        this.$emit('update:startDate', newValue.toDate())
      },
      deep: true
    },
    endDateLocal: {
      handler (newValue) {
        this.$emit('update:endDate', newValue.toDate())
      },
      deep: true
    }
  },
  created () {
    if (this.rangeStartAutoAlign) {
      this.startDateLocal = moment(this.startDate).startOf(this.rangeType)
      this.endDateLocal = moment(this.startDate).endOf(this.rangeType)
    } else {
      this.startDateLocal = moment(this.startDate).startOf('day')
      this.endDateLocal = moment(this.startDate).add(1, this.rangeType).subtract(1, 'day').endOf('day')
    }
  },
  methods: {
    nextRange () {
      this.startDateLocal.add(1, this.rangeType)
      this.endDateLocal.add(1, this.rangeType)
      this.$set(this.startDateLocal, '__force_update', !this.startDateLocal.__force_update)
      this.$set(this.endDateLocal, '__force_update', !this.endDateLocal.__force_update)
    },
    previousRange () {
      this.startDateLocal.subtract(1, this.rangeType)
      this.endDateLocal.subtract(1, this.rangeType)
      this.$set(this.startDateLocal, '__force_update', !this.startDateLocal.__force_update)
      this.$set(this.endDateLocal, '__force_update', !this.endDateLocal.__force_update)
    }
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
