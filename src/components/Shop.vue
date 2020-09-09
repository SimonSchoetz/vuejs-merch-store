<template>
  <div class="shop">
    <div>
    <h1>Shop</h1>
      <ProductCard 
        v-for="(product, i) in stock" 
        @add-to-cart="updateCart" 
        :key="i" 
        :merch-stock="product" 
      />
    </div>
    <Cart />

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
  }},
  methods: {
    updateCart(input) {
      console.log(this.cart)
      this.cart.push(input);
    }
  },
  computed: {
    cartAmmount() {
      return this.cart.length
    }
  },
  components: {
      ProductCard,
      Cart
  }
}
</script>

