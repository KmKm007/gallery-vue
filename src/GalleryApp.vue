<template>
  <div id="app">
    <div class="nav">
      <nav-item v-for="i in amount" key="i"></nav-item>
    </div>
  </div>
</template>

<script>
import GalleryElement from './components/gallery-element'
import NavItem from './components/nav-item'
import data from './data/imageDatas.json'
export default {
  data () {
    return {
      data
    }
  },
  name: 'galleryApp',
  components: {
    GalleryElement,
    NavItem
  },
  computed: {
    amount () {
      return data.length
    }
  },
  methods: {
  }
}
</script>

<style language="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.nav {
  width: 100%;
  display: flex;
  justify-content: center;
  position: fixed;
  left: 0;
  bottom: 50px;
}
</style>
