<template>
  <div id="app">
    <SimonGame/>
  </div>
</template>

<script>
import SimonGame from './components/SimonGame.vue'

export default {
  name: 'App',
  components: {
    SimonGame
  }
}
</script>

<style lang="sass">
*
  margin: 0
  padding: 0
  box-sizing: border-box
  
  body
    display: block  
    height: 100%   
    padding: 10px
</style>
