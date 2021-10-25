<template lang="pug">
div.indicators-wrapper
  span(v-for="i in indicators" :key="i" :class="[getIndicatorClass(i)]" :data-id="i") 
</template>
<script>
import {ref, watch} from 'vue'
export default {
  props: {
    length: {
      type: Number,
      required: true,
    },
    current: {
      type: Number,
      required: true,
    },
    maxVisibleIndicators: {
      type: Number,
      default: 4,
      validator: (val) => val >=3
    }
  },
  setup(props) {
    const indicators = ref(Array.from({length: props.length}, (v, k) => k))
    const min = ref(0)
    const max = ref(props.maxVisibleIndicators)
    const getIndicatorClass = (ref) => {
      if (ref === props.current) {
      return 'active';
      }

      if ( ref === min.value  && ref - 1 >= 0 || ref === max.value && ref + 1 < props.length) {
        return 'micro';
      }

      if (ref === min.value + 1 && ref - 2 >= 0 ||  ref === max.value -1 && ref + 2 < props.length) {
        return 'small';
      }

      if (ref >= min.value && ref <= max.value) {
        return 'std';
      }
      
      return 'hidden';
    }

    const calculate = () => {

      if (min.value - 1 >= 0 ) {
        if (props.current === min.value) {
          min.value = props.current - 1
          max.value = min.value + props.maxVisibleIndicators
        }

        if (props.current === min.value + 1) {
          min.value = props.current - 2
          max.value = min.value + props.maxVisibleIndicators
        }

        if (max.value > props.length) {
          max.value = props.length - 1
        }
      }


      if (max.value + 1 < props.length) {
        if (props.current === max.value) {
          max.value = props.current + 1
          min.value = max.value - props.maxVisibleIndicators
        }
        if (props.current === max.value - 1) {
          max.value = props.current + 2
          min.value = max.value - props.maxVisibleIndicators
        }
        if (min.value < 0) {
          min.value = 0
        }
      }
    }
  
    watch(() => props.current, calculate)
    watch(() => props.maxVisibleIndicators, calculate)

    return {
      indicators,
      getIndicatorClass
    }
  },
}
</script>
<style scoped lang="sass">
  .indicators-wrapper
    display: flex
    justify-content: center
    align-items: center
    span
      width: 10px
      height: 10px
      margin: 2px
      border-radius: 50%
      background-color: #EEEEEE
      overflow: hidden
      transition: all 500ms ease-out
      text-indent: -9999px
      &:first-child
        margin-left: 20px
      &:last-child
        margin-right: 20px
    .active
      background-color: red
    .small
      width: 6px
      height: 6px
      margin: 4px
      &:first-child
        margin-left: 10px
      &:last-child
        margin-right: 10px
    .micro
      width: 4px
      height: 4px
      margin: 6px
    .hidden
      width: 0
      height: 0
      margin: 4px 0
</style>