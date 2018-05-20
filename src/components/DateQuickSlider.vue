<template>
  <div class="date-quick-slider" :class="'slider-type-' + rangeType">
    <div class="slider-control" @click="previousRange()">
      <back-svg></back-svg>
    </div>
    <div class="slider-date" :style="sliderDateStyle">
      {{startDateLocalFormatted}} - {{endDateLocalFormatted}}
    </div>
    <div class="slider-control" @click="nextRange()">
      <forward-svg></forward-svg>
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
    // TODO: To be implemented
    startDateLimit: {
      validator: (value) => {
        return moment(value)._isValid
      }
    },
    // TODO: To be implemented
    endDateLimit: {
      validator: (value) => {
        return moment(value)._isValid
      }
    },
    displayFormat: {
      type: String,
      default: () => 'D MMM'
    }
  },
  computed: {
    startDateLocalFormatted () {
      return this.startDateLocal.format(this.displayFormat)
    },
    endDateLocalFormatted () {
      return this.endDateLocal.format(this.displayFormat)
    },
    sliderDateStyle () {
      var characters = this.displayFormat.length + 1
      if (this.rangeType !== 'day') {
        characters = characters * 2 + 3
      }
      if (this.displayFormat) {
        return 'min-width:' + characters + 'ch;'
      }
    }
  },
  watch: {
    startDateLocal (newValue) {
      this.$emit('update:startDate', newValue.toDate())
    },
    endDateLocal (newValue) {
      this.$emit('update:endDate', newValue.toDate())
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
      var startDateLocalTemp = this.startDateLocal.add(1, this.rangeType)
      var endDateLocalTemp = this.endDateLocal.add(1, this.rangeType)
      // workaround for not able to trigger vue to detect changes.
      this.startDateLocal = undefined
      this.endDateLocal = undefined
      this.startDateLocal = startDateLocalTemp
      this.endDateLocal = endDateLocalTemp
    },
    previousRange () {
      var startDateLocalTemp = this.startDateLocal.subtract(1, this.rangeType)
      var endDateLocalTemp = this.endDateLocal.subtract(1, this.rangeType)
      // workaround for not able to trigger vue to detect changes.
      this.startDateLocal = undefined
      this.endDateLocal = undefined
      this.startDateLocal = startDateLocalTemp
      this.endDateLocal = endDateLocalTemp
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
  .date-quick-slider {
    display: flex;
    .slider-control {
      display: inline-flex;
      svg {
        width: 30px;
        transition: all 300ms ease;
        align-self: center;
        &:hover {
          fill: red;
        }
      }
    }
    .slider-date {
      display: inline-block;
      text-align: center;
      align-self: center;
      user-select: none;
    }
  }
</style>
