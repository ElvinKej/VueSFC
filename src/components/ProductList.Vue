<template>
    <div><h1>Welcome to the Product List Page</h1>
        <div v-for="product in sortedProducts" class="lessons">
        <h1 v-text="product.subject"></h1>
        </div>
    </div>
</template>

<script>
export default {
    name: "ProductList",
    props: ["sortedProducts"],
}