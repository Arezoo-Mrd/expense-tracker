<template>
    <h3>History</h3>
    <ul id="list" class="list">
        <li v-bind:class="transaction.amount > 0 ? 'plus' : 'minus'" v-for="transaction in transactions"
            :key="transaction.id">
            {{ transaction.text }}
            <span class="">
                ${{ transaction.amount }}
            </span>
            <button class="delete-btn" @click="deleteTransactions(transaction.id)">X</button>

        </li>

    </ul>
</template>

<!-- <script>
export default {
    setup() {
        const transactions = [
            { id: 1, text: 'Flower', amount: -19.99 },
            { id: 2, text: 'Salary', amount: 299.97 },
            { id: 3, text: 'Book', amount: -10 },
            { id: 4, text: 'Camera', amount: 150.99 }
        ]
        return {
            transactions
        }
    }
    // data() {
    //     return {
    //         transactions: [
    //             { id: 1, text: 'Flower', amount: -19.99 },
    //             { id: 2, text: 'Salary', amount: 299.97 },
    //             { id: 3, text: 'Book', amount: -10 },
    //             { id: 4, text: 'Camera', amount: 150.99 }
    //         ]
    //     }
    // },
    // methods: {

    // }
}
</script> -->

<!-- 
<script setup>
const transactions = [
    { id: 1, text: 'Flower', amount: -19.99 },
    { id: 2, text: 'Salary', amount: 299.97 },
    { id: 3, text: 'Book', amount: -10 },
    { id: 4, text: 'Camera', amount: 150.99 }
]

</script> -->

<script setup>
import { defineProps } from 'vue';
const props = defineProps({
    transactions: {
        type: Array,
        required: true
    }
})
const emit = defineEmits(['deleteTransaction'])
const deleteTransactions = (transactionId) => {
    emit("deleteTransaction", transactionId)
}
</script>
