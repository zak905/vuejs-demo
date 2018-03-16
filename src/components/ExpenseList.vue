<template>
  <div class="expense-list">
      <table class="expense-table">
          <thead>
              <th>Amount</th>
              <th>Date</th>
              <th>VAT rate %</th>
              <th>VAT</th>
              <th>Reason</th>
          </thead>
          <tbody>
              <tr v-for="expense in expenses">
                  <td>{{ expense.amount + getCurrencySymbol(expense.currency, currencies)}}</td>
                  <td>{{ expense.date }}</td>
                  <td>{{ expense.vatRate }}</td>
                  <td>{{ expense.vat + getCurrencySymbol(expense.currency, currencies)}}</td>
                  <td>{{ expense.reason }}</td>
              </tr>

          </tbody>
      </table>
  </div>
</template>

<script>
export default {
  name: 'ExpenseList',
  props: {
    currencies: Array,
    expenses: Array,
    vatRate: String
  },
  computed: {
      totalVat: (amount) => {return this.vatRateAsNumber * amount;},
      vatRateAsNumber: () => {return Number.parseInt(this.vatRate) / 100;}
  },
  methods: {
      getCurrencySymbol: (currencyName, currencies) => {
            for (let i = 0; i < currencies.length; i++ ) {
            if (currencyName === currencies[i].name)
                      return currencies[i].symbol;
          }  
          return "$"
          }
  }
}
</script>

<style scoped>
.expense-list{
    margin: auto;
    max-width: 400px;
}
.expense-table {
    border: solid 1px black;
    min-width: 400px;
}
</style>
