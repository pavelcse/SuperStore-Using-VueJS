<template>
    <ul class="list-group">
        <li class="list-group-item">
            <span class="item-name">Name</span>
            <span class="item-price float-right">Price</span>
        </li>
    <hr>
        <li v-for="(item, index) in items" :key="index" class="list-group-item">
            <button @click="removeItem(index)" class="btn btn-danger btn-sm">X</button>
            <span class="item-name">{{ item.title }}</span>
            <span class="item-price float-right">${{ item.price }}</span>
        </li>
    <hr>
        <li class="list-group-item">
            <span class="item-name">Total</span>
            <span class="item-price float-right">${{ totalPrice }}</span>
        </li>
        <li v-if="items.length > 0" class="list-group-item">
            <button @click="checkout" class="btn btn-block btn-success btn-sm"> Checkout </button>
        </li>
    </ul>
</template>

<script>
export default {
    computed: {
        items() {
            return this.$store.getters.getCart
        },
        totalPrice() {
            var total = 0
            this.items.forEach(item => {
                total += parseFloat(item.price)
            })
            return total.toFixed(2)
        }
    },
    methods: {
        removeItem(index) {
            this.$store.commit('removedItem', index)
        },
        checkout() {
            if(confirm('Are You Sure to Checkout?')){
                this.$store.commit('clearCart')
            }
        }
    }
}
</script>

<style>

</style>
