<template>
    <div><h2>Welcome to the Checkout</h2></div>
<!-- 
<h3>Your current items in the cart are {{totalItemsInTheCart}} in total:</h3>
<div v-for="product in sortedProducts">
<div v-if="atLeastOneInTheCart(product)">
<h3 v-text="product.title"></h3>
<p><span>Product ID:</span>{{ "" + product.id }}</p>
</div>
</div> -->


</template>

<!-- <script>
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
   }
}

</script> -->