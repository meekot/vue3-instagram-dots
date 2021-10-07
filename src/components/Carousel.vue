<template lang="pug">
div 
  div 
    button(@click="decrement" :disabled="!allowDecrement" style="margin-right:10px") Previous
    button(@click="increment" :disabled="!allowIncrement") Next
  CarouseIndicator(:current="current" :length="length")
</template>
<script>
import CarouseIndicator from './CarouseIndicator.vue'
import {ref, computed} from 'vue'
export default {
  setup() {
    const length = 15
    const current = ref(0)
    const increment = () => current.value += 1
    const decrement = () => current.value -= 1
    const allowIncrement = computed(() => current.value < length-1)
    const allowDecrement = computed(() => current.value > 0)
    return {
      length,
      current,
      increment,
      decrement,
      allowIncrement,
      allowDecrement,
    }
  },
  components: {
    CarouseIndicator

  }
}
</script>