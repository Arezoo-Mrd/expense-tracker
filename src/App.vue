<template>
  <Header />
  <div class="container">
    <Balance :total="total" />
    <IncomeExpenses :income="+income" :expense="+expense" />
    <TransactionList :transactions="transactions" @deleteTransaction="handleDeleteTransaction" />
    <AddTransaction @transactionSubmitted="handleTransactionSubmitted" />
  </div>
</template>

<script setup>
import Header from "./components/Header.vue"
import Balance from "./components/Balance.vue"
import IncomeExpenses from "./components/IncomeExpenses.vue"
import TransactionList from "./components/TransactionList.vue"
import AddTransaction from "./components/AddTransaction.vue"
import { ref, computed, onMounted } from "vue"
import { useToast } from "vue-toastification"

const transactions = ref([])


const toast = useToast()
//  Get total
const total = computed(() => {
  return transactions.value.reduce((acc, transaction) => {
    return acc + transaction.amount
  }, 0)
})

// Get income
const income = computed(() => {
  return transactions.value
    .filter(transaction => transaction.amount > 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount
    }, 0)
})

//  Get expense
const expense = computed(() => {
  return transactions.value
    .filter(transaction => transaction.amount < 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount
    }, 0)
})

const handleTransactionSubmitted = (transacitionData) => {
  transactions.value.push({
    id: generateUniqueId(),
    ...transacitionData
  })

  toast.success("Add Transaction Successfully")

}
const generateUniqueId = () => {
  return Math.floor(Math.random() * 1000000)
}

const handleDeleteTransaction = (transactionId) => {
  transactions.value = transactions.value.filter((transaction) => transaction.id !== transactionId)
  toast.success("Transaction Deleted Successfully")

}
// export default {
//   components: {
//     Header,
//     Balance,
//     IncomeExpenses,
//     TransactionList,
//     AddTransaction
//   }
// }
</script>

