<template>
  <div class="products">
    <h1>Products</h1>
        <ProductCard v-for="(product, i) in stock" :key="i" :merch-stock="product" />
  </div>
</template>

<script>
import merchDB from "../merch.json";
import ProductCard from  "./ProductCard"
export default {
  name: 'Products',
  data() { return {
        stock: merchDB
  }},
  methods: {
  },
  components: {
      ProductCard
  }
}
</script>

