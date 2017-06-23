<template lang="html">
  <div class="elements">
    <g-element
      v-for="i in amount"
      :data="datas[i-1]"
      :position="positions[i-1]"
      :deg="degs[i-1]"
      :key="i-1"
      :index="i-1"
      :isInverse="isInverses[i-1]"
      :isCenter="activeIndex === (i-1)"
      :handleClick="handleElementClick"
    />
  </div>
</template>

<script>
import GElement from './g-element'

export default {
  name: 'g-element-container',
  props: {
    amount: {
      type: Number,
      required: true
    },
    datas: {
      type: Array,
      required: true
    },
    positions: {
      type: Array,
      required: true
    },
    degs: {
      type: Array,
      required: true
    },
    isInverses: {
      type: Array,
      required: true
    },
    activeIndex: {
      type: Number,
      required: true
    },
    handleElementClick: {
      type: Function,
      required: true
    }
  },
  components: {
    GElement
  }
}
</script>

<style lang="css">
</style>
