<template>
  <div>
    <MuseumHighlight />
  </div>

</template>

<script>
import MuseumHighlight from './components/MuseumHighlight.vue'

export default {
  name: 'App',
  components: {
    MuseumHighlight,
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: -8px;
}

//I added the links class here as it is supposed to work on all pages and all links throughout the website
.links {
  text-decoration: none;
  color: black;
}

.links:hover {
  text-decoration: underline;
}
</style>
