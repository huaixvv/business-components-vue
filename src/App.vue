<template>
  <div id="app">
    <remote-select></remote-select>
  </div>
</template>

<script>
import remoteSelect from './components/remoteSelect.vue'

export default {
  name: 'App',
  components: {
    remoteSelect
  }
}
</script>

<style lang="less">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
