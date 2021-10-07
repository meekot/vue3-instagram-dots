<template lang="pug">
div.indicators-wrapper
  span(v-for="i in indicators" :key="i" :class="[getIndicatorClass(i)]" :data-id="i") 
</template>
<script>
import {ref, watch} from 'vue'
const MAX_VISIBLE_INDICATORS = 4
export default {
  props: {
    length: {
      type: Number,
      required: true,
    },
    current: {
      type: Number,
      required: true,
    }
  },
  setup(props) {
    const indicators = ref(Array.from({length: props.length}, (v, k) => k))
    const min = ref(0)
    const max = ref(MAX_VISIBLE_INDICATORS)
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
  
    watch(() => props.current, (val) => {

      console.log('wtf')

      if (min.value - 1 >= 0 ) {
        if (val === min.value) {
          min.value = val - 1
          max.value = min.value + MAX_VISIBLE_INDICATORS
        }

        if (val === min.value + 1) {
          min.value = val - 2
          max.value = min.value + MAX_VISIBLE_INDICATORS
        }

        if (max.value > props.length) {
          max.value = props.length - 1
        }
      }


      if (max.value + 1 < props.length) {
        if (val === max.value) {
          max.value = val + 1
          min.value = max.value - MAX_VISIBLE_INDICATORS;
        }
        if (val === max.value - 1) {
          max.value = val + 2
          min.value = max.value - MAX_VISIBLE_INDICATORS;
        }
        if (min.value < 0) {
          min.value = 0
        }
      }


      console.log(min.value, max.value, val)

    })
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
      width: 5px
      height: 5px
      margin: 2px
      border-radius: 50%
      background-color: #d3d3d3
      overflow: hidden
      transition: all 500ms ease-out
      text-indent: -9999px
      &:first-child
        margin-left: 20px
      &:last-child
        margin-right: 20px
    .active
      width: 8px
      height: 8px
      margin: 1px
      background-color: blue
    .small
      width: 4px
      height: 4px
      margin: 3px
      &:first-child
        margin-left: 10px
      &:last-child
        margin-right: 10px
    .micro
      width: 2px
      height: 2px
      margin: 4px
    .hidden
      width: 0
      height: 0
      margin: 4px 0
</style>