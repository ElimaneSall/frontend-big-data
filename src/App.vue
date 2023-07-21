<template>
  <div id="app">
    <div class="conts">
      <Dash_board/>
    </div>
    
  </div>
</template>

<script>
import Dash_board from './components/Dashboard.vue'

export default {
  name: 'App',
  components: {
    Dash_board
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 20px;
}

</style>
