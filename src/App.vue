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
      :sortedProducts="sortedProducts" 
      :cart="cart" @add-item-to-cart="addItemToCart"
      @manage-remove-item="manageRemoveItem"></component>
    </main>
  </div>
</template>

<script>
import ProductLesson from './components/ProductLesson.vue';
import Checkout from './components/Checkout.vue';
//import products from './assets/json/products.json'


export default {
  name: 'App',
  data() {
    return {
      sitename: "Vue.js SFC App",
      cart: [],
      currentView: ProductLesson,
      //products: products,
      //imagesBaseURL:"",
      products: [],
      AWS_URL: "https://webstorev1-env.eba-kvhfmh8p.eu-west-2.elasticbeanstalk.com/collections/products",
    }
  },
  components: {
    ProductLesson, Checkout
  },
  created: function() {
    let webstore = this;
    fetch(this.AWS_URL).then(
      function (response) {
        response.json().then(
          function (json) {
            console.log(json);
            webstore.products = json;
          }
        )
      }
    )
    // if ("serviceWorker" in navigator) {
    //   navigator.serviceWorker.register("service-worker.js");
    // }
  },
  methods: {
    showCheckout() {
      if (this.currentView === ProductLesson) {
        this.currentView = Checkout;
      } else {
        this.currentView = ProductLesson;
      }
    },
    addItemToCart: function (product) {
      this.cart.push(product.id);
    },
    removeItemFromCart(product) {
      let index= this.cart.indexOf(product.id);
      this.cart.splice(index, 1);
    },
    manageRemoveItem(product) {
      this.removeItemFromCart(product);
      if(!this.atLeastOneInTheCart) {
        this.currentView = ProductLesson;
      }
    },
    atLeastOneInTheCart() {
      return this.totalItemsInTheCart >= 1;
    }
    // addItemToCart: function (selectedProduct) {
    //   let x = parseFloat(selectedProduct.space);
    //   let cartLess = structuredClone(selectedProduct);
    //   if (x > 0) {
    //     x = x - 1;
    //     cartLess.space = 1;
    //     this.cart.push(cartLess);
    //     selectedProduct.space = x;
    //   }
    // }
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
