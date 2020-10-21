<template>
  <div class="shop">
      <h1>Busted Fingerz Merch</h1>
      <!-- <img class="busted-gif" src="../assets/busted_gif.gif" /> -->
      <div class="fake-nav">
        <h2 :class="activeCart ? '' : 'active'" >PRODUCTS</h2>
        <h2 :class="activeCart ? 'active' : ''" @click="showCart(true)">CART ({{cartAmount}})</h2>
      </div>
    <div v-show="activeCart" class="coming-soon" @click="showCart(false)">
      <h2>COMMING SOON!</h2>
    </div>
    <div class="body">
      <div class="products-component">
        <ProductCard 
          v-for="(product, i) in stock" 
          @add-to-cart="updateCart" 
          :key="i" 
          :merch-stock="product" 
        />
      </div>
      <Cart :cartItems="cart" />
    </div>
  </div>
</template>

<script>
import merchDB from "../merch.json";
import ProductCard from  "./ProductCard";
import Cart from "./Cart";
export default {
  name: 'Shop',
  data() { return {
        stock: merchDB,
        cart: [],
        activeCart: false
  }},
  methods: {
    updateCart(input) {
      console.log(this.cart)
      this.cart.push(input);
    },
    showCart(input) {
      this.activeCart = input;
      console.log(this.activeCart)
    }
  },
  computed: {
      cartAmount() {
        return this.cart.length
      }
    
  },
  components: {
      ProductCard,
      Cart
  }
}
</script>

