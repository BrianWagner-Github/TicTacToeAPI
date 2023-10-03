<template>
  <div id="TicTacToe">
    <TicTacToeBoard/>
  </div>
</template>

<script>
import TicTacToeBoard from './components/TicTacToeBoard'

export default {
  name: 'TicTacToe',
  components: {
    TicTacToeBoard
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
  margin-top: 60px;
}
</style>
