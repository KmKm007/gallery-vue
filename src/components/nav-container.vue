<template lang="html">
  <div class="nav">
    <nav-item
      v-for="i in amount"
      :key="i - 1"
      :isActive="activeIndex === i - 1"
      :index="i - 1"
      :handleClick="onIndexChange"
    />
  </div>
</template>

<script>
import NavItem from './nav-item'

export default {
  name: 'nav-container',
  props: {
    amount: {
      type: Number,
      required: true
    },
    activeIndex: {
      type: Number,
      required: true
    },
    onIndexChange: {
      type: Function,
      required: true
    }
  },
  components: {
    NavItem
  },
  methods: {
  }
}
</script>

<style lang="css">
.nav {
  width: 100%;
  display: flex;
  justify-content: center;
  position: fixed;
  left: 0;
  bottom: 50px;
}
</style>
