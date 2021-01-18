<template>
  <div id="app">
    <WorkSheet/>
  </div>
</template>

<script>
import WorkSheet from './components/WorkSheet.vue'

export default {
  name: 'App',
  components: {
    WorkSheet
  }
}
</script>

<style>
#app {
  font-family: 'Open Sans';
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
