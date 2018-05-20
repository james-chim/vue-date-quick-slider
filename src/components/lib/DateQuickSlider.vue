<template>
  <div class="date-quick-slider" :class="'slider-type-' + rangeType">
    <div class="slider-control" @click="previousRange()">
      <back-svg></back-svg>
    </div>
    <div class="slider-date" :style="sliderDateStyle" :class="sliderDateClass">
      <div class="slider-date-previous" :style="sliderDateStyle">
        {{startDateLocalPreviousFormatted}}<span v-show="rangeType!=='day'"> - {{endDateLocalPreviousFormatted}}</span>
      </div><!--
   --><div class="slider-date-current" :style="sliderDateStyle">
        {{startDateLocalFormatted}}<span v-show="rangeType!=='day'">  - {{endDateLocalFormatted}}</span>
      </div><!--
   --><div class="slider-date-next" :style="sliderDateStyle">
        {{startDateLocalNextFormatted}}<span v-show="rangeType!=='day'">  - {{endDateLocalNextFormatted}}</span>
      </div>
    </div>
    <div class="slider-control" @click="nextRange()">
      <forward-svg></forward-svg>
    </div>
  </div>
</template>

<script>
import backSvg from '../../assets/ion-ios-back.svg'
import forwardSvg from '../../assets/ion-ios-forward.svg'

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
      endDateLocal: undefined,
      slidingDirection: undefined
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
    startDateLocalNextFormatted () {
      return this.startDateLocal.clone().add(1, this.rangeType).format(this.displayFormat)
    },
    endDateLocalNextFormatted () {
      return this.endDateLocal.clone().add(1, this.rangeType).format(this.displayFormat)
    },
    startDateLocalPreviousFormatted () {
      return this.startDateLocal.clone().subtract(1, this.rangeType).format(this.displayFormat)
    },
    endDateLocalPreviousFormatted () {
      return this.endDateLocal.clone().subtract(1, this.rangeType).format(this.displayFormat)
    },
    sliderDateStyle () {
      var characters = this.displayFormat.length + 1
      if (this.rangeType !== 'day') {
        characters = characters * 2 + 3
      }
      return 'width:' + characters + 'ch;'
    },
    sliderDateClass () {
      if (this.slidingDirection) {
        return 'moving-' + this.slidingDirection
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
      this.slidingDirection = 'next'
      setTimeout(() => {
        var startDateLocalTemp = this.startDateLocal.add(1, this.rangeType)
        var endDateLocalTemp = this.endDateLocal.add(1, this.rangeType)
        // workaround for not able to trigger vue to detect changes.
        this.startDateLocal = undefined
        this.endDateLocal = undefined
        this.startDateLocal = startDateLocalTemp
        this.endDateLocal = endDateLocalTemp
        this.slidingDirection = undefined
      }, 200)
    },
    previousRange () {
      this.slidingDirection = 'previous'
      setTimeout(() => {
        var startDateLocalTemp = this.startDateLocal.subtract(1, this.rangeType)
        var endDateLocalTemp = this.endDateLocal.subtract(1, this.rangeType)
        // workaround for not able to trigger vue to detect changes.
        this.startDateLocal = undefined
        this.endDateLocal = undefined
        this.startDateLocal = startDateLocalTemp
        this.endDateLocal = endDateLocalTemp
        this.slidingDirection = undefined
      }, 200)
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
      > svg {
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
      user-select: none;
      align-self: center;
      overflow: hidden;
      white-space: nowrap;
      > div {
        user-select: none;
        display: inline-block;
        text-align: center;
        transform: translateX(-100%);
      }
      &.moving-next > div,
      &.moving-previous > div {
        transition: transform 0.2s ease;
      }
      &.moving-next > div{
        transform: translateX(-200%);
      }
      &.moving-previous > div{
        transform: translateX(0);
      }
    }
  }
</style>
