<template>
  <div class="products">
    <h1>Products</h1>
    
  </div>
</template>

<script>
import merchDB from "../merch.json"

export default {
  name: 'Products',
  data() {
       return {
           stock: merchDB,
    }
  },
  methods: {
  },
  props: {
    // msg: String
  }
}
</script>

