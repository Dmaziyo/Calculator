<template>
  <div id="app">
      <calculator></calculator>
  </div>
</template>

<script>
import Calculator from './components/Calculator'

export default {
  name: 'App',
  components: {Calculator}
}
</script>

<style>
#app {
  text-align: center;
  margin-top: 60px;
}
</style>
