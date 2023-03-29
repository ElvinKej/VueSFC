<template>
    <div><h1>Welcome to the Product Lesson Page</h1>
        <div v-for="product in sortedProducts" class="lessons">
        <h1 v-text="product.subject"></h1>
        <figure>
            <img v-bind:src="imagesBaseURL + product.image">
        </figure>
        </div>
    </div>
</template>

<script>
export default {
    name: "ProductLesson",
    props: ["sortedProducts", "imagesBaseURL"],
}