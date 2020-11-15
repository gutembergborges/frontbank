<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p>
      For a guide and recipes on how to configure / customize this project,<br>
      check out the
    </p>
    
    <h3>Developed by Gutemberg Borges in VueJS</h3>
    <ul>
      <li><a href="https://github.com/gutembergborges/frontbank" target="_blank" rel="noopener">GitHub</a></li>
      <li><a href="https://github.com/gutembergborges" target="_blank" rel="noopener">Gutemberg Borges</a></li>
      <li><a href="https://vuejs.org/" target="_blank" rel="noopener">Vue.js</a></li>
      <li><a href="https://www.capgemini.com/" target="_blank" rel="noopener">Capgemini</a></li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'BankTerminal',
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
