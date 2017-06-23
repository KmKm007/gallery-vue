<template lang="html">
  <span :class="classNames" @click="handleClick(index)"></span>
</template>

<script>
import cs from 'classnames'

export default {
  props: {
    index: {
      type: Number,
      required: true
    },
    isActive: {
      type: Boolean,
      required: true
    },
    handleClick: {
      type: Function,
      required: true
    }
  },
  computed: {
    classNames () {
      return cs({
        'nav-item': true,
        'nav-item-active': this.isActive
      })
    }
  }
}
</script>

<style lang="css">
.nav-item {
  background-color: #e5e5e5;
  width: 16px;
  height: 16px;
  border-radius: 50%;
  margin-left: 25px;
  cursor: pointer;
  transition: transform .5s;
}

.nav-item-active {
  background-color: #999999;
  transform: scale(1.5, 1.5);
}
</style>
