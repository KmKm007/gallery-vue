<template>
  <div id="app" class="container">
    <g-element-container
      :amount="amount"
      :activeIndex="activeIndex"
      :datas="datas"
      :degs="degs"
      :positions="positions"
      :isInverses="isInverses"
      :handleElementClick="onIndexChange"
    />
    <nav-container
      :amount="amount"
      :activeIndex="activeIndex"
      :onIndexChange="onIndexChange"
    />
  </div>
</template>

<script>
import GElementContainer from './components/g-element-container'
import datas from './data/imageDatas.json'
import { getRandom } from './utils/MathUtil'
import NavContainer from './components/nav-container'

export default {
  data () {
    return {
      datas: null,
      isInitial: true,
      positions: null,
      degs: null,
      isInverses: null,
      amount: null,
      activeIndex: 0,
      width: null,
      height: null,
      eleWidth: null,
      eleHeight: null
    }
  },
  name: 'galleryApp',
  components: {
    GElementContainer,
    NavContainer
  },
  created () {
    this.initial()
  },
  mounted () {
    setTimeout(this.reverse.bind(this), 0)
  },
  computed: {
  },
  methods: {
    initial () {
      this.width = 1280
      this.height = 700
      this.eleWidth = 320
      this.eleHeight = 360
      this.datas = datas
      this.amount = this.datas.length
      this.positions = this.getPostions()
      this.degs = this.getDegs()
      this.isInverses = this.getInverse()
    },
    createPosition () {
      const { width, height, eleWidth, eleHeight } = this
      const halfWidth = width / 2
      const halfHeight = height / 2
      const halfEleWidth = eleWidth / 2
      const halfEleHeight = eleHeight / 2
      let poiX = parseInt(getRandom(0, width))
      let poiY
      if (poiX > (halfWidth - eleWidth) && poiX < (halfWidth + eleWidth)) {
        poiY = getRandom(0, halfHeight - eleHeight)
      } else {
        poiY = parseInt(getRandom(0, height))
      }
      return [poiX - halfEleWidth, poiY - halfEleHeight]
    },
    createDeg () {
      const deg = Math.random() * 60 - 30
      return deg
    },
    getPostions (isInitial = true) {
      const { amount, activeIndex, width, height } = this
      const createPosition = this.createPosition.bind(this)
      const positions = []
      for (let i = 0; i < amount; i++) {
        if (isInitial) {
          positions.push([0, 0])
        } else if (activeIndex === i) {
          positions.push([width / 2 - 150, height / 2 - 160])
        } else {
          positions.push(createPosition())
        }
      }
      return positions
    },
    getDegs (isinitial = true) {
      const amount = this.amount
      const createDeg = this.createDeg
      const degs = []
      if (!isinitial) {
        for (let i = 0; i < amount; i++) {
          degs.push(createDeg())
        }
      } else {
        for (let i = 0; i < amount; i++) {
          degs.push(0)
        }
      }
      return degs
    },
    getInverse () {
      const amount = this.amount
      const isInverses = []
      for (let i = 0; i < amount; i++) {
        isInverses.push(false)
      }
      return isInverses
    },
    onIndexChange (index) {
      if (this.activeIndex === index) {
        this.$set(this.isInverses, index, !this.isInverses[index])
      } else {
        this.isInverses = this.getInverse()
        this.activeIndex = index
        this.reverse()
      }
    },
    reverse () {
      this.positions = this.getPostions(false)
      this.degs = this.getDegs(false)
    }
  }
}
</script>

<style language="scss">
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  padding: 0;
  font-family: sans-serif;
}

.container {
  position: relative;
  height: 100vh;
  overflow: hidden;
  background-color: #cccccc;
}

.back {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  background-color: #fff;
  transform: rotateY(180deg) translateZ(1px);
  backface-visibility: hidden;
  padding: 0 20px;
}

.figure {
  position: relative;
}

</style>
