<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/capgemini-logo.svg">
    <BankTerminal msg="Bank Terminal"/>
  </div>
</template>

<script>
import BankTerminal from './components/BankTerminal.vue'

export default {
  name: 'App',
  components: {
    BankTerminal
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
