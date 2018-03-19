<template>
  <div id="app">
    <img src="./assets/logo.png">
    <div>
      <label for="vat"> VAT in %</label>
      <input id="vat" type="number" v-model="vatRate">
    </div>
     <ExpenseForm :currencies="currencies" :vatRate="vatRate" :expenses="expenses" />
     <div class="divider"></div>
     <ExpenseList :currencies="currencies" :expenses="expenses"/>
  </div>

</template>

<script>
import ExpenseForm from './components/ExpenseForm.vue'
import ExpenseList from './components/ExpenseList.vue'

export default {
  name: 'app',
  components: {
    ExpenseForm,
    ExpenseList
  },
   data: () => ({
     vatRate: 20,
    expenses: [],
    currencies: [{name: "EUR", symbol: "€"}, {name: "USD", symbol: "$"}, {name: "GBP", symbol: "£"}],
  }),
  
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
.divider {
  height: 30px;
}
</style>
