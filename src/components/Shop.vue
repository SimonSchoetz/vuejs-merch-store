<template>
  <div class="shop">
      <h1>Busted Fingerz Merch</h1>
      <!-- <img class="busted-gif" src="../assets/busted_gif.gif" /> -->
      <div class="fake-nav" v-show="!showCheckout">
        <h2 :class="activeCart ? '' : 'active'"  @click="showCart(false)">PRODUCTS</h2>
        <h2 :class="activeCart ? 'active' : ''" @click="showCart(true)">CART ({{cartAmount}})</h2>
      </div>
    <!-- <div v-show="activeCart" class="coming-soon" @click="showCart(false)">
      <h2>COMMING SOON!</h2>
    </div> -->
    <div class="body">
      <div v-show="!showCheckout">
        <div v-show="!activeCart" class="products-component">
          <ProductCard 
            v-for="(product, i) in stock" 
            @add-to-cart="updateCart" 
            :key="i" 
            :merch-stock="product" 
          />
        </div>
        <div v-show="activeCart" class="cart-component">
          <Cart 
            :cartItems="cart"
            @set-checkout="setShowCheckout" 
          />
        </div>
      </div>
      <div v-show="showCheckout" class="checkout-component">
        <Checkout @set-checkout="setShowCheckout" />
      </div>
    </div>
  </div>
</template>

<script>
import merchDB from "../merch.json";
import ProductCard from  "./ProductCard";
import Cart from "./Cart";
import Checkout from "./Checkout";

export default {
  name: 'Shop',
  data() { return {
        stock: merchDB,
        cart: {
          includes: [],
          items: []
        },
        activeCart: false,
        showCheckout: false
  }},
  methods: {
    updateCart(input) {
      if (!this.cart.includes.includes(input)) {
        this.cart.includes.push(input)
        this.cart.items.push({item: input, amount: 1})
      } else {
        this.cart.items.forEach(item => {
          if (item.item === input) {item.amount ++}
        })
      }
      console.log(this.cart.items);
    },
    showCart(input) {
      this.activeCart = input;
    },
    setShowCheckout() {
      this.showCheckout = !this.showCheckout;
      console.log(this.showCheckout)
    }
  },
  computed: {
      cartAmount() {
        let amountItems = 0;
        this.cart.items.forEach(item => {
          amountItems += item.amount
        })
        return amountItems
      },
      // sortedCart() {
      //   const isInCart = [];

      // }
    
  },
  components: {
      ProductCard,
      Cart,
      Checkout
  }
}
</script>

