<template>
  <div class="products">
    <h1>Products</h1>
    <Product :merch-stock="stock" />
  </div>
</template>

<script>
import merchDB from "../merch.json";
import Product from  "./Product"
console.log(merchDB)
export default {
  name: 'Products',
  data() { return {
        stock: merchDB
  }},
  methods: {
  },
  components: {
      Product
  }
}
</script>

