<template>
    <div><h2>Welcome to the Checkout</h2>

<h3>Your current items in the cart are {{totalItemsInTheCart}} in total:</h3>
    <div>
        <div v-for="product in sortedProducts" class="lessons">
            <div v-if="atLeastOneInTheCart(product)">
                <p>Subject: {{product.subject}} </p>
                <p>Location: {{product.location}} </p>
                <p>Price: {{product.price}}</p>
                <p>Space: {{product.space}}</p>
                <img v-bind:src="product.image">
            <p>Available items:{{ itemsLeft(product) }}</p>
            <p>In the cart you have added: {{ cartCount(product.id) }}</p>
    <!-- <h3 v-text="product.subject"></h3>
    <p><span>Product ID:</span>{{ "" + product.id }}</p> -->
    <button @click="manageRemoveItem(product)">Remove 1 product</button>
    </div>
    </div>
</div>
</div>

</template>

<script>
export default {
    name: "Checkout",
    props: ["sortedProducts", "cart"],
   methods: {
    cartCount(id) {
        let count = 0;
        for (let i = 0; i < this.cart.length; i++) {
            if (this.cart[i] === id) {
                count++;
            }
        }
        return count;
    },
    itemsLeft(product) {
        return product.space - this.cartCount(product.id);
    },
    atLeastOneInTheCart(product) {
        return  this.cart.includes(product.id);
    },
   },
   computed: {
    totalItemsInTheCart: function () {
        return this.cart.length || ";"
    },
    manageRemoveItem: function (product) {
        this.$emit("manage-remove-item", product);
    }
   }
};
</script>