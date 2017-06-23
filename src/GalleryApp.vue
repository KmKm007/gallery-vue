<template>
  <div id="app" class="container">
    <gallery-element
      v-for="i in amount"
      :data="datas[i-1]"
      :position="positions[i-1]"
      :deg="degs[i-1]"
      :key="i-1"
      :index="i-1"
      :isInverse="isInverses[i-1]"
      :isCenter="activeIndex === i-1"
    />
    <div class="nav">
      <nav-item v-for="i in amount" key="i"></nav-item>
    </div>
  </div>
</template>

<script>
import GalleryElement from './components/gallery-element'
import NavItem from './components/nav-item'
import datas from './data/imageDatas.json'
import { getRandom } from './utils/MathUtil'

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
    GalleryElement,
    NavItem
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
      console.log(positions)
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
      const { activeIndex, isInverses } = this
      if (activeIndex === index) {
        isInverses[index] = !isInverses[index]
      } else {
        const isInverses = this.getInverse()
        this.activeIndex = index
        this.isInverses = isInverses
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

.nav {
  width: 100%;
  display: flex;
  justify-content: center;
  position: fixed;
  left: 0;
  bottom: 50px;
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

.nav-item-active {
  background-color: #999999;
  transform: scale(1.5, 1.5);
}
</style>
