<template lang="html">
  <div
    :class="className"
    :style="style"
  >
    <div class="front">
      <div>
        <img :src="photoSrc"/>
      </div>
      <div class="front-title">
        {{data.title}}
      </div>
    </div>
    <div class="back">
        {{data.desc}}
    </div>
  </div>
</template>

<script>
import cs from 'classnames'

export default {
  props: ['data', 'position', 'deg', 'isInverse', 'isCenter', 'handleClick'],
  computed: {
    className () {
      return cs({
        'element': true,
        'inverse': this.isInverse,
        'center': this.isCenter
      })
    },
    style () {
      return {
        left: `${this.position[0]}px`,
        top: `${this.position[1]}px`,
        transform: this.isCenter ? '' : `rotate(${this.deg}deg)`
      }
    },
    photoSrc () {
      return require(`../images/${this.data.fileName}`)
    }
  }
}
</script>

<style lang="scss">
$animate-during: .8s;
$animate-style: ease-in-out;

.element {
  width: 320px;
  height: 360px;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #fff;
  position: absolute;
  transition: left $animate-during $animate-style, top $animate-during $animate-style, transform $animate-during $animate-style;
  cursor: pointer;
  color: #a7a0a2;
  transform-style: preserve-3d;
}

.inverse {
  transform: rotateY(180deg);
}

.center {
  z-index: 9999;
}

.front {
}

.front-title {
  margin-top: 10px;
}
</style>
