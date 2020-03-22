<template>
  <div id="app">
    <bingo-grid></bingo-grid>
  </div>
</template>

<script>
import BingoGrid from './components/BingoGrid'

export default {
  name: 'app',
  components: {
    BingoGrid
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 0;
  padding: 0;
}
</style>
