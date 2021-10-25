<template lang="pug">
.carousel 
  .carousel-inner
    .carousel-inner--control.control__prev(v-if="!hideControl")
      slot(name="prev-control" :prev="decrement" :disabled="!allowDecrement")  
        .default
          button.value(@click="decrement" :disabled="!allowDecrement") ◄
    transition-group(tag="div" class="carousel-inner--container" :name="'carousel-slide' + (backDirection? 'back' : '')" :style="{height, width}")
      .carousel-inner--container__item(v-for="index in [current]" :key="index" :style="{height, width}")
        slot(v-if="index === current" name="item" :item="itemList[index]")
    .carousel-inner--control.control__next(v-if="!hideControl")
      slot(name="next-control" :next="increment" :disabled="!allowIncrement")
        .default
          button(@click="increment" :disabled="!allowIncrement") ►
  CarouseIndicator(v-if="!hideControl" :current="current" :length="length" :maxVisibleIndicatorsProp="maxVisibleIndicatorsProp - 1")
</template>
<script>
import CarouseIndicator from './CarouseIndicator.vue'
import {ref, computed} from 'vue'
export default {
  props: {
    itemList: {
      type: Array,
      default: () => []
    },
    width: {
      type: String,
      default: '100%'
    },
    height: {
      type: String,
      default: '100px'
    },
    maxVisibleIndicatorsProp: {
      type: Number,
      default: 5,
      validator: (val) => val > 3
    },
    activeItemIndexProp: {
      type: Number,
      default: 0,
    }
  },
  setup(props) {
    const length = computed(() => props.itemList.length)
    const current = ref(0)
    const backDirection = ref(false)
    const hideControl = computed(() => length.value === 1)
    const increment = () => {
      backDirection.value = false
      current.value += 1
    }
    const decrement = () => {
      backDirection.value = true
      current.value -= 1
    }
    const allowIncrement = computed(() =>  current.value < length.value - 1)
    const allowDecrement = computed(() => current.value > 0)
    return {
      length,
      current,
      increment,
      decrement,
      hideControl,
      allowIncrement,
      allowDecrement,
      backDirection
    }
  },
  components: {
    CarouseIndicator
  }
}
</script>
<style lang="sass" scoped>
.carousel 
  display: flex
  flex-direction: column
  align-items: center
  .carousel-inner 
    display: flex
    margin-bottom: 10px
    .carousel-inner--control 
      .default
        height: 100%
        display: flex
        font-size: 40px
        align-items: center
        button 
          font-size: 35px
          padding: 0px
          margin: 0px
          background: transparent
          border: none
          cursor: pointer
          
          &:hover
            opacity: 0.6
    &--container 
      overflow: hidden
      position: relative
      &__item 
        position: absolute
      
      .carousel-slide 
        &-leave-active,
        &-enter-active,
        &back-leave-active,
        &back-enter-active 
          transition: 1s
        
        &-enter-active
          transform: translate(100%, 0)
        
        &-enter-to 
          transform: translate(0, 0)

        &-leave-to 
          transform: translate(-100%, 0)
        

        &back-enter-active 
          transform: translate(-100%, 0)
        &back-enter-to 
          transform: translate(0, 0)
        &back-leave-to 
          transform: translate(100%, 0)
</style>