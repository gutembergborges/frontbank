<template>
  <div class="terminal">
    <header>
      <h1>{{ title }}</h1>
    </header>


    <h3>
      <label for="operation">Escolha a operação que deseja realizar: </label>
      <select id="operation" v-model="operation" name="operation">
        <option>Consultar Saldo</option>
        <option>Depósito</option>
        <option>Saque</option>
      </select>
    </h3>

    <h2> {{ operation }} </h2>
    
    <div class="form">
      <p v-if="errors.length">
        <b>Por favor, verifique o(s) seguinte(s) dado(s):</b>
        <ul>
          <li v-for="error in errors" :key="error">{{ error }}</li>
        </ul>
      </p>

      <p>
        <label for="number">Conta Corrente: </label>
        <input id="number" v-model="number" type="text" name="number">
      </p>
      <p v-if="operation == 'Depósito' || operation == 'Saque'">
        <label for="value">Valor: </label>
        <input id="value" v-model="value" type="text" name="value">
      </p>
      <p>
        <button @click="checkForm">Confirmar</button>
      </p>
    </div>

    <div v-if="result.number != null && result.balance != null" class="result-operation">
      <h3>Resultado da Operação</h3>
      <h4>Conta Corrente: </h4>{{ result.number }}
      <h4>Saldo Disponível: </h4>{{ result.balance }}
    </div>
    <div v-else-if="typeof result == 'string'">
      {{ result }}
    </div>

    <footer>
      <h3>Desenvolvido por Gutemberg Borges em VueJS</h3>
      <ul>
        <li><a href="https://github.com/gutembergborges/frontbank" target="_blank" rel="noopener">GitHub</a></li>
        <li><a href="https://github.com/gutembergborges" target="_blank" rel="noopener">Gutemberg Borges</a></li>
        <li><a href="https://vuejs.org/" target="_blank" rel="noopener">Vue.js</a></li>
        <li><a href="https://www.capgemini.com/" target="_blank" rel="noopener">Capgemini</a></li>
      </ul>
    </footer>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'BankTerminal',
  props: {
    title: String,
  },
  data () {
    return {
      accounts: [],
      errors: [],
      operation: "Consultar Saldo",
      number: null,
      value: null,
      result: {number: null, balance: null}
    }
  },
  mounted () {
    axios
      .get('http://localhost:8000/api/accounts/')
      .then(response => (this.accounts = response.data))
  },
  methods:{
    checkForm: function () {
      this.errors = [];
      
      if (this.number && this.operation == 'Consultar Saldo') {
        this.submitOperation()
      } else if (this.number && this.value && this.operation != 'Consultar Saldo') {
        this.submitOperation()
      } else {
        this.result = {number: null, balance: null}

        if (!this.number) {
          this.errors.push('O número da Conta Corrente é obrigatório.')
        }
        if (!this.value && this.operation != 'Consultar Saldo') {
          this.errors.push('É preciso informar o valor da operação.')
        }

      }
    },
    submitOperation: function () {
      if(this.operation == 'Consultar Saldo') {
        axios
          .get('http://localhost:8000/api/accounts/'+this.number)
          .then(response => (this.result = response.data))
      } else if(this.operation == 'Depósito') {
        axios
          .put('http://localhost:8000/api/accounts/deposit/'+this.number, { balance: this.value })
          .then(response => {
            this.result = response.data
          })
      } else {
        axios
          .put('http://localhost:8000/api/accounts/draw/'+this.number, { balance: this.value })
          .then(response => {
            this.result = response.data
          })
      }
    }
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
  color: #2c3e50;
}
</style>
