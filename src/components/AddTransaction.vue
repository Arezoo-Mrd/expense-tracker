<template>
    <h3>Add new transaction</h3>
    <form id="form" @submit.prevent="onSubmit">
        <div class="form-control">
            <label for="text">Text</label>
            <input type="text" v-model="text" id="text" placeholder="Enter text...">
        </div>
        <div class="form-control">
            <label for="amount">Amount <br />
                (negative - expense, positive - income)</label>
            <input type="number" v-model="amount" id="amount" placeholder="Enter amount...">
        </div>
        <button class="btn">Add transaction</button>
    </form>
</template>

<script setup>
import { ref } from "vue"
import { useToast } from "vue-toastification";
const toast = useToast()
const text = ref('')
const amount = ref(0)

const emit = defineEmits(['transactionSubmitted'])
const onSubmit = () => {
    if (!text.value.trim() || !amount.value) {
        toast.error("Please enter text and amount")
        return
    }
    const transacitionData = {
        text: text.value,
        amount: amount.value
    }

    emit("transactionSubmitted", transacitionData)

    text.value = ''
    amount.value = 0
}
</script>