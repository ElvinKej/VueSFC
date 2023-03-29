<!-- <template>
  <div id="app">
    <header>
      <h1></h1>
        <button @click="showCheckout">{{ this.cart.length }}
        Checkout</button>
    </header>
    <main>
      <component :is="currentView"></component>
    </main>
  </div>
</template>
<script>
import ProductList from "./components/ProductList.Vue";
import Checkout from "./components/Checkout.vue";

export default {
  name: "App"
}
</script> -->

<template>
  <div id="app">
    <header>
      <h1>{{ sitename }}</h1>
      <button @click="showCheckout">{{ totalItemsInTheCart }}Checkout
      <font-awesome-icon icon="fa-solid fa-cart-shopping"/>
      </button>
    </header>
      

    <main>
      <component :is="currentView"
      :sortedProducts="sortedProducts"></component>
    </main>
  </div>
</template>

<script>
import ProductList from './components/ProductList.vue';
import Checkout from './components/Checkout.vue';
import products from "./assets/json/products.json";


export default {
  name: 'App',
  data() {
    return {
      sitename: "Vue.js SFC App",
      cart: [],
      currentView: ProductList,
      products: products,
      //products: [],
    }
  },
  components: {
    ProductList, Checkout
  },
  methods: {
    showCheckout() {
      if (this.currentView === ProductList) {
        this.currentView = Checkout;
      } else {
        this.currentView = ProductList;
      }
    }
  },
  computed: {
    totalItemsInTheCart: function() {
      return this.cart.length || "";
    },
    sortedProducts() {
      function compare(a, b) {
        if (a.subject > b.subject) return 1;
        if (a.subject < b.subject) return -1;
        return 0;
      }
      return this.products.sort(compare);
    }
  }
};
</script>

<!-- <style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style> --> 
