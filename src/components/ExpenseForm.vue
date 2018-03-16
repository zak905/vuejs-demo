<template>
  <div class="expense-form">
    <label for="amount">Amount: </label>
    <input type="number" id="amount" v-model="amount"/>
    <label for="amountVAT">VAT: </label>
    <input type="number" id="amountVAT" v-model="amountVAT" disabled/>
    <label for="currency">Currency: </label>
    <select id="currency" v-model="currency">
      <option v-for="currency in currencies"> {{ currency.name }} </option>  
    </select>
    <label for="date"  >Date: </label>
    <input type="date" id="date" value="2018/03/06" v-model="date"/>
    <label for="reason">Reason: </label>
    <textarea id="reason" v-model="reason" />
    <button id="append" v-on:click="submitExpense"> Add Expense </button>
  </div>
</template>

<script>
export default {
  name: 'ExpenseForm',
  methods: {
    submitExpense: function(event) {
        this.expenses.push({"amount": this.amount, "date": this.date, "reason": this.reason, "vatRate": this.vatRate, "vat": this.amountVAT, "currency": this.currency});
    }
  },
  data: () => {
      return {
      amount: 0,
      date: '',
      reason: '',
      amountVAT: 0,
      currency: ''
      }
  },
  props: {
    currencies: Array,
    expenses: Array,
    vatRate: String,
  },
    
    watch: {
        amount: function (amount) {
        this.amountVAT = parseFloat(Number.parseInt(this.vatRate) / 100 * this.amount).toFixed(2)
        },
        vatRate: function (amount) {
        this.amountVAT = parseFloat(Number.parseInt(this.vatRate) / 100 * this.amount).toFixed(2)
        }
    },
created: () => {console.log(this.vatRate)}
}
</script>

<style scoped>
.expense-form {
 margin: auto;
 display: flex;
 max-width: 400px;
 flex-direction: column;
}
button {
  background: green;
  color: floralwhite;
  margin: auto;
  min-height: 50px;
  margin-top: 20px;
}
</style>
