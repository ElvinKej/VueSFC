<template>
    <div><h1>Welcome to the Product Lesson Page</h1>
        <div v-for="product in sortedProducts" class="lessons">
        <p>Subject: {{product.subject}} </p>
        <p>Location: {{product.location}} </p>
        <p>Price: {{product.price}}</p>
        <p>Space: {{product.space}}</p>
        <figure>
        <img v-bind:src="imagesBaseURL + product.image">
    </figure>
        <button v-if="canAddToCart(product)" v:on:click="addItemToCart(product)">Add to the Cart</button>
            <button disabled v-else>Add to Cart</button>

            <span v-if="itemsLeft(product) === 0">Out of Stock!</span>
            <span v-else-if="itemsLeft(product) < 5">Only {{itemsLeft(product)}} remaining</span>
            <span v-else>Buy now!</span>
        </div>
    </div>
</template>

<script>
export default {
    name: "ProductLesson",
    props: ["sortedProducts", "imagesBaseURL","cart"],
    data() {
        return {}
    },
    methods: {
        canAddToCart(product) {
            return product.space > this.cartCount(product.id);
        },
        cartCount(id) {
            let count = 0;
            for (let i = 0; i < this.cart.length; i++) {
                if (this.cart[i] === id) {
                    count++;
                }
            }
            return count;
        },
        addItemToCart: function (product) {
            this.$emit("add-item-to-cart", product);
        },
        itemsLeft(product) {
            return product.space - this.cartCount(product.id);
        },
    }
}
</script>